# 1 - 77

public final class MyGameStateFactory implements Factory<GameState> {

	@Nonnull @Override public GameState build(GameSetup setup, Player mrX, ImmutableList<Player> detectives) {
      return new MyGameState(setup, ImmutableSet.of(Piece.MrX.MRX), ImmutableList.of(), mrX, detectives);
	}

	private final class MyGameState implements GameState {
        private GameSetup setup;
        private ImmutableSet<Piece> remaining;
        private ImmutableList<LogEntry> log;
        private Player mrX;
        private List<Player> detectives;
        private ImmutableSet<Move> moves;
        private ImmutableSet<Piece> winner;
		private ImmutableList<Player> everyone;

		//"The final keyword ensures the reference to the MrX travel log is immutable, preventing it from being reassigned. Meanwhile, the ImmutableList type ensures the contents of the log remain read-only and cannot be modified.

        private MyGameState(
                final GameSetup setup,
                final ImmutableSet<Piece> remaining, // all the pieces that haven't moved yet
                final ImmutableList<LogEntry> log,
                final Player mrX,
                final List<Player> detectives) {

            // CHECKS
            if (setup == null) throw new NullPointerException();
            if (setup.moves.isEmpty()) throw new IllegalArgumentException("Moves is empty!");
            if (setup.graph.edges().isEmpty()) throw new IllegalArgumentException("Graph is empty!");
            if (detectives.isEmpty()) throw new IllegalArgumentException("Detectives is empty!");
            if (!mrX.piece().isMrX()) throw new IllegalArgumentException("MrX should be Mrx");
            if (!mrX.isMrX()) throw new IllegalArgumentException("there is no mrX!");
            // check properties of each detective
            for (Player d : detectives) {
                if (!d.isDetective()) throw new IllegalArgumentException("No detective!");
                if (d.has(ScotlandYard.Ticket.DOUBLE))
                    throw new IllegalArgumentException("detectives can.t have double");
                if (d.has(ScotlandYard.Ticket.SECRET))
                    throw new IllegalArgumentException("detectives shouldn't have secret ticket");
            }

    // 检查位置是否重复  
           Set<Integer> locations = new HashSet<>();
           for (Player d : detectives) {
           if (!locations.add(d.location())) {
           throw new IllegalArgumentException("Duplicate location found!");
    }
}

            // create a list with all the players (detectives + mrx)
            List<Player> everyone = new ArrayList<>();
            everyone.add(mrX);
            everyone.addAll(detectives);

            this.setup = setup;
            this.remaining = remaining;
            this.log = log;
            this.mrX = mrX;
            this.detectives = detectives;
			this.everyone = ImmutableList.copyOf(everyone);
            this.winner = getWinner();
            this.moves = getAvailableMoves();
		}	







# 80 - 95
		@Nonnull
        @Override
        public GameSetup getSetup() {
            return setup;       //body
        }

        @Nonnull
        @Override
        public ImmutableSet<Piece> getPlayers() {
            List<Piece> all = new ArrayList<>();   //List （interface）is make some get add and size function
            all.add(mrX.piece());                  //  ArrayList(class) is a real thing 
            for (Player i : detectives) {
                all.add(i.piece());
            }
            return ImmutableSet.copyOf(all);
        }

getPlayers() ： get Interface methods by myself
@Nonnull ：
 an Annotation(注解) ,This method is declared to never return null
 public : access permission
 setup : object name
 GameSetup : the return type

Immutable (cannot be modified and only read)
Set : <1>If you try to put two things in , it will only keep one.  <2> disorder
List<Piece> all = new ArrayList<>(); arrayList   new ：Instantiation（）

for : Loop statement
player i : Temporary variable
. : Dot Operator  add ‘s function



# 97 - 130
       @Nonnull
        @Override
        public ImmutableSet<Piece> getWinner() {   // 预先准备好所有侦探棋子的集合，方便在侦探赢的时候返回
         ImmutableSet<Piece> detectivePieces = detectives.stream()  // Incoming data
            .map(Player::piece)                    // 进：Player, 出：Piece  map : Convert转换
            .collect(ImmutableSet.toImmutableSet());  // collect 收集 ， ImmutableSet Class or type ， toImmutableSet() ：Static Method 
                                                       //它是定义在 ImmutableSet 这个类里面的。    它的作用是产生一个 Collector（收集器）


         // 1. 侦探赢：是否有任何侦探的位置与 MrX 重合
         if (detectives.stream().anyMatch(d -> d.location() == mrX.location())) { 
         return detectivePieces;
        }
		//anyMatch Once an element satisfies the condition, it stops further checks and returns true.

         // 2. 侦探赢：轮到 MrX 走，但他已经无路可走（Single 和 Double 都为空）
         if (remaining.contains(mrX.piece()) &&
            makeSingleMoves(setup, detectives, mrX, mrX.location()).isEmpty() &&
            makeDoubleMoves(setup, detectives, mrX, mrX.location(), log).isEmpty()) {
         return detectivePieces;
         }
		 // && : and 
		 //如果集合里一个元素都没有，它就返回 true   只要他没法移动，他就输了

         // 3. MrX 赢：没有任何侦探还能移动（所有侦探都动不了了）
         if (detectives.stream().allMatch(d -> makeSingleMoves(setup, detectives, d, d.location()).isEmpty())) {
         return ImmutableSet.of(mrX.piece());
         } //anyMatch Once an element satisfies the condition, it stops further checks and returns true.

     // 4. MrX 赢：旅行日志已填满，且轮到了 MrX（意味着侦探已经错过了最后一次抓捕机会）
      if (log.size() == setup.moves.size() && remaining.contains(mrX.piece())) {
        return ImmutableSet.of(mrX.piece());
        }

		//log.size()：Mr.X 已经走过的步数（也就是当前进行到了第几轮）。
        //setup.moves.size()：游戏设定的总步数
		//remaining.contains(mrX.piece()) 当前轮到 Mr.X 行动

        // 游戏尚未结束
        return ImmutableSet.of();
}






# 130 - 140
        @Nonnull 
        @Override
        public Optional<Integer> getDetectiveLocation(Piece.Detective detective) {  //Parameter type， mean i need//detective ：Parameter
            for (Player p : detectives) {
                if (p.piece().equals(detective)) 
                    return Optional.of(p.location());
            }
            return Optional.empty();
        }
optional 两个选择 ： 如果是这个侦探的棋子，那么返回这个棋子的位置， 没找到就给个空盒





# 141 - 153
@Nonnull
		@Override
		public Optional<TicketBoard> getPlayerTickets(Piece piece) {
			if (piece == mrX.piece())
				return Optional.of(t -> mrX.tickets().get(t));

			for (Player d : detectives) {
				if (d.piece() == piece)
					return Optional.of(t -> d.tickets().get(t));
			}
			return Optional.empty();
		}

如果是mrx ticket  放在
t -> 这个是lambda 方法
board.java 里 



# 154 - 160
@Nonnull
		@Override
		public ImmutableList<LogEntry> getMrXTravelLog() {
			return log;
		}

Mr.X generates a LogEntry every time he moves.有ticket and location




# 161 - 196
private static ImmutableSet<SingleMove> makeSingleMoves(
        GameSetup setup, List<Player> detectives, Player player, int source) {

          Set<Integer> occupiedLocations = detectives.stream()
            .map(Player::location)
            .collect(Collectors.toSet());

            return setup.graph.adjacentNodes(source).stream()
            .filter(destination -> !occupiedLocations.contains(destination))

			//transport ： formal parameter of the Lambda expression（就是点到点之间connection）it is temporary name
            //.filter ： true or false ,if ture then keep it the next step , if false then throw away, but not Modify data
            //.map :  transform  form the transport to the singlemove 包含了：谁、从哪、用什么票、去哪

            .flatMap(destination -> {
           List<SingleMove> moves = new ArrayList<>(); //Interface Type //Variable Name //Keyword //Implementation //（）Constructor


             setup.graph.edgeValueOrDefault(source, destination, ImmutableSet.of())
			//游戏的“地图”  //connection information              这个方法不会返回 null

               .forEach(transport -> {       //  .forEach： Looping terminal operations   transport ：Lambda Parameter
                if (player.has(transport.requiredTicket())) {   //Conditional Statement
                    moves.add(new SingleMove(player.piece(), source, transport.requiredTicket(), destination));  //Method Call
                }
            });


                if (player.has(ScotlandYard.Ticket.SECRET)) {
                moves.add(new SingleMove(player.piece(), source, ScotlandYard.Ticket.SECRET, destination));
    }// move ： object reference ,add method , (...)Argument
          return moves.stream();  // 将篮子里的东西转成 Stream 返回给 flatMap
          })
            .collect(ImmutableSet.toImmutableSet());  //Terminal Operation ：collector         最后收集为不可变集合
}



# 198 - 226
        private static Set<DoubleMove> makeDoubleMoves(
        GameSetup setup,
        List<Player> detectives,
        Player player,
        int source,
        ImmutableList<LogEntry> log) {

    // 1. 基础条件检查：必须有双步票，且游戏剩余轮数足够   （setup.moves.size() 减去当前已走的 log.size()）必须至少还有 2 轮
    if (!player.has(Ticket.DOUBLE) || setup.moves.size() - log.size() < 2) {   
        return Collections.emptySet();
    }

    // 2. 使用 Stream 组合两步移动
    return makeSingleMoves(setup, detectives, player, source).stream()
        .flatMap(m1 -> {
            // 模拟第一步执行后的玩家状态（扣票、换位置）
            Player playerAfterFirst = player.use(m1.ticket).at(m1.destination);
            
            // 计算从第一步终点出发的所有合法第二步
            return makeSingleMoves(setup, detectives, playerAfterFirst, m1.destination).stream()
                .map(m2 -> new DoubleMove(
                        player.piece(), 
                        source, 
                        m1.ticket, m1.destination, 
                        m2.ticket, m2.destination
                ));
        })
        .collect(Collectors.toSet());  //Delete repeat and keep only one.
}








# 254-258:  @Nonnull
		@Override
		public GameState advance(Move move) {
			if (!moves.contains(move))
				throw new IllegalArgumentException("Illegal move: " + move);

			return move.accept(new Move.Visitor<GameState>() {
Logical NOT: ! 会把结果反过来
Dot Operator: moves.contains 调用 moves 的 contains 方法。
moves (复数)：是游戏规则生成的“合法动作列表”。（前面定义的）
Move (单数/类型)：是定义“动作”该长什么样的规范/模板。
move (变量名)：是玩家选中的那个具体数据包

accept 作用是 Dispatch instructions
if move is single move 它内部的 accept 方法会执行 visitor.visit(this)，从而进入你写的处理单步移动的逻辑
如果 move 实际上是一个 DoubleMove，它会执行对应的 visit(DoubleMove) 逻辑。
返回结果：无论走哪条路，最终都会返回一个新的 GameState 给 advance 方法。
new Move.Visitor<GameState>
new + Anonymous Inner Class

Move.Visitor： The Move interface defines an internal interface called Visitor.
接口强制你必须实现两个方法：visit(SingleMove m) 和 visit(DoubleMove m)。
<GameState> (泛型) 意思：这个 Visitor 在处理完移动后，必须交出一个 GameState 类型的结果。


# 262 - 278 public GameState visit(Move.SingleMove m) {
					if (m.commencedBy().isMrX()) {         
						Player newMrX = mrX.use(m.ticket).at(m.destination);

						LogEntry entry = setup.moves.get(log.size())
								? LogEntry.reveal(m.ticket, m.destination)
								: LogEntry.hidden(m.ticket);

						ImmutableList<LogEntry> newLog = ImmutableList.<LogEntry>builder()
								.addAll(log).add(entry).build();

						ImmutableSet<Piece> newRemaining = ImmutableSet.copyOf(
								detectives.stream().map(Player::piece).collect(Collectors.toList()));

						return new MyGameState(setup, newRemaining, newLog, newMrX, detectives);
					} else 

commencedBy(): 检查棋子是否是mrx
Player newMrX = mrX.use(m.ticket).at(m.destination); use消耗票数，at更新地址

LogEntry entry = setup.moves.get(log.size())
        ? LogEntry.reveal(m.ticket, m.destination)
        : LogEntry.hidden(m.ticket);

		//log.size() 指当前走的第几步
		//setup.move.get 获取预设的boolean
		//if true ，will reveal
		//if false ， will hidden

		ImmutableList<LogEntry> newLog = ImmutableList.<LogEntry>builder()
        .addAll(log).add(entry).build();

	   //.addAll(log) 导入旧数据
	   //.add(entry)  加新数据
       //.build()  让内容不可修改
	   //newlog  is a new object 
	   //Builder 就像是一个临时的“购物筐”
	   //<LogEntry> (泛型) //专门用来装LogEntry（日志条目）对象的 


ImmutableSet<Piece> newRemaining = ImmutableSet.copyOf(
        detectives.stream().map(Player::piece).collect(Collectors.toList()));

		//order: who is next one can move
		//player -> player.piece()       get the player piece
		.collect(Collectors.toList())  collect the piece and pagage it in the list

return new MyGameState(setup, newRemaining, newLog, newMrX, detectives);  
// return the new MyGameState 



# 278 - 300 List<Player> newDetectives = detectives.stream()
					List<Player> newDetectives = detectives.stream()
                    .map(d -> d.piece() == m.commencedBy() ? d.use(m.ticket).at(m.destination) : d)
                    .collect(Collectors.toList());

					//detectives.stream 把侦探放在stream
					//(condition ? result A : result B)         ternary operator
					//condition:   d.piece() == m.commencedBy()   检查这个侦探是不是这个m move
					//result A： d.use(m.ticket).at(m.destination) yes   take a ticket and at a destination
					//result B: stay as is (保留原样)
					//collect(Collectors.toList())      package in the Lsit<Player>

                    Player newMrX = mrX.give(m.ticket);
					//侦探每用一张交通票，这张票必须交给 MrX


		 // 步骤 A: 从“待行动列表”中移除刚刚走过的侦探
        Set<Piece> remainingPieces = remaining.stream()
        .filter(p -> p != m.commencedBy())              //只要“不等于当前行动者”的棋子
        .collect(Collectors.toCollection(HashSet::new)); //将过滤后的结果放入一个新的 HashSet

       // 步骤 B: 检查剩下的侦探是否还能动
        remainingPieces.removeIf(p -> newDetectives.stream() 
        .filter(d -> d.piece() == p)  //从更新后的侦探列表中，找到棋子为 p 的那个侦探对象（为了获取他最新的位置和车票信息）。
        .findFirst()  //查找：只要找到第一个
        .map(d -> makeSingleMoves(setup, newDetectives, d, d.location()).isEmpty())  // calculate the available move
        .orElse(true)); //找不到这个侦探


		ImmutableSet<Piece> newRemaining = remainingPieces.isEmpty()
								? ImmutableSet.of(Piece.MrX.MRX)
								: ImmutableSet.copyOf(remainingPieces);

						return new MyGameState(setup, newRemaining, log, newMrX, newDetectives);

		condition ： remainingPieces.isEmpty()
		result A: true, 轮到 MrX 行动
		result B:  不为空  返回 remainingPieces 继续侦探回合

		return new MyGameState(setup, newRemaining, log, newMrX, newDetectives);

# 300 - 329 public GameState visit(Move.DoubleMove m) {
		Player newMrX = mrX
        .use(ScotlandYard.Ticket.DOUBLE) // 扣除一张双倍票
        .use(m.ticket1)                 // 扣除第一步的交通票
        .use(m.ticket2)                 // 扣除第二步的交通票
        .at(m.destination2);            // 最终位置定格在第二站

		LogEntry entry1 = setup.moves.get(log.size()) // 检查当前步是否该现身
        ? LogEntry.reveal(m.ticket1, m.destination1)
        : LogEntry.hidden(m.ticket1);

LogEntry entry2 = setup.moves.get(log.size() + 1) // 检查下一步是否该现身
        ? LogEntry.reveal(m.ticket2, m.destination2)
        : LogEntry.hidden(m.ticket2);

		ImmutableList<LogEntry> newLog = ImmutableList.<LogEntry>builder()
        .addAll(log)
        .add(entry1) // 按顺序压入第一步
        .add(entry2) // 按顺序压入第二步
        .build();


		ImmutableSet<Piece> newRemaining = ImmutableSet.copyOf(
        detectives.stream().map(Player::piece).collect(Collectors.toList()));

return new MyGameState(setup, newRemaining, newLog, newMrX, detectives);


# 重点

（1）.stream (Start the pipeline) //Provides an interface for performing functional operations
（2）.map (Convert or transform) (key, value)
             .get(key) 是用来根据键 (Key) 获取对应值 (Value) 的方法 
（3）.collect (Pack)  //Reconstruct into a collection (such as a List, Set, or ImmutableSet).
（4）.findFirst() (Terminal Operation) //Return the first element in the stream that satisfies the previous condition 
                 //if not found then return Optional.empty()    Avoid nullpointerexception
（5）.filter //If the conditions are met, proceed to the next step; otherwise, discard it.

（7） :: (Method Reference)    //Player::piece   （the logic is exactly the piece method inside the Player class.）
      -> (lambda)             //player -> player.piece() (take a player object and retrieve its piece.)
（8）.anyMatch()             //It finds the first element that satisfies the condition, halts the traversal immediately, and returns true
    .allMatch               // all element
	.noneMatch               //all element can't 
（9）.contains()      //For collections such as Sets or Lists        
    .has()            //For an object of type Player
	remaining.contains(mrX.piece())  //Does the set “remaining” contain the object mrX.piece()?
(10) ImmutableSet.of(a, b, c)   //Ensure that the game data remains unchanged  
    ImmutableSet.copyOf(somecollection) //
	set  //Duplicate elements are not allowed， it is disorder   (like HashSet, ImmutableSet)
	list  //Allow duplicate elements， Keep the order in which you inserted them (like ArrayList, ImmutableList)
	ImmutableSet.Builder （Constructor/Factory） 
	ImmutableSet （Container）
（11）Optional<T> //A “box that may be empty”
    泛型 (Generics)  <T> //Type placeholder(You can put anything in there like integer, string)
(12)(Piece piece) (Type Parameter Name)
（13）static
（14）.collect(Collectors.toSet());
Collectors：  Tools provided by Java
toSet()： Put these elements into a Set
（15）List<SingleMove> moves = new ArrayList<>();
//List<SingleMove> moves：这是声明Declaration   I defined a variable named moves to store SingleMove objects.
//new ArrayList<>()：这是实例化（Instantiation） order to Store data
（16）



