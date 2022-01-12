# Design a chess game

![Chess](chess.JPG?raw=true)

## System requirements :

1. Till the game is ACTIVE, players have to take their turn.

2. In each turn, take move input from the user and if the move is valid, allow move.

3. Continue the game until a player wins the game or the game is a draw. (Consider only CheckMate and StaleMate condition)

4. Handle Check conditions.


# Position
```java
public class Position {
   private int x, y;
	
   public Position(int x, int y) {
       this.x = x;
       this.y = y;
   }
   public int getX() {
       return this.x;
   }
   public int getY() {
       return this.y;
   }
}
```

# Move
```java
public class Move {
    private Position src, dest;
	
    public Position getSrc() {
	return src;
    }

    public Position getDest() {
	return dest;
    }

    //Initialize setters.
}
```

# Piece
```java
public abstract class Piece {
     private Position pos;
     public final boolean isWhite;
     private boolean isAlive;
	
     public Piece(boolean isWhite) {
	  this.isWhite = isWhite;
	  this.isAlive = true;
     }
	
     public void setPosition(Position pos) {
	  this.pos = pos;
     }
	
     public Position getPosition() {
	  return this.pos;
     }
	
     public void setIsAlive(boolean isAlive) {
	  this.isAlive = isAlive;
     }

     public boolean getIsAlive() {
	  return isAlive;
     }
	
     public abstract boolean checkMove(Position dest);
}
```

# Knight
```java
public class Knight extends Piece{
	
     public Knight(boolean isWhite) {
	 super(isWhite);
     }
	
     public boolean checkMove(Position dest) {
	 if(dest.x < 0 || dest.x > 7 || dest.y < 0 || dest.y > 7) {
		return false;
	 }
		
	 //If current piece can move to that position.
	 int[] tx = new int[]{-2, -2, -1, 1, 2, 2, 1, -1};
	 int[] ty = new int[]{-1, 1, 2, 2, 1, -1, -2, -2};
	 boolean result = false;
		
	 for(int i = 0; i < 8; i++) {
	     int x = this.position.getX() + tx[i];
	     int y = this.position.getY() + ty[i];
	     if(x >= 0 && x < 8 && y >= 0 && y < 8 && x == dest.x && y == dest.y) {
		result = true;
	     }
	 }
		
	return result;
     }
}
```

# Player
```java
public class Player {
     private final boolean isWhite;
     private King king;
     private Queen queen;
     private Knight[] knights;
	
     public Player(boolean isWhite) {
	  this.isWhite = isWhite;
	  this.king = new King(isWhite);
	  this.queen = new Queen(isWhite);
	  this.knights = new Knight[2];
	  this.knights[0] = new Knight(isWhite);
          this.knights[1] = new Knight(isWhite);
     }

     //Initialize setters and getters.
	
     public Move takeMoveInput() {
	  Move move = new Move();
	  //Take inputs from user and put those inputs in move object.
	  return move;
     }

     public void showOutput(GameStatus status) {
	  //Show output according to the status.
     }
}
```

# GameStatus
```java
public enum GameStatus {
    ACTIVE,
    ERROR,
    CHECK,
    DRAW,
    BLACK_WINS,
    WHITE_WINS;
}
```

# ChessBoard 
```java
public class ChessBoard {
     private Piece[][] board;
     public ChessBoard(Player black, Player white) {
	  this.board = new Piece[8][8];
	  
          this.board[0][1] = white.getKnight(0);
	  white.getKnight(0).setPosition(new Position(0, 1));
	  this.board[0][6] = white.getKnight(1);
	  white.getKnight(1).setPosition(new Position(0, 6));
	  this.board[0][3] = white.getQueen();
	  white.getQueen().setPosition(new Position(0, 3));
	  this.board[0][4] = white.getKing();
	  white.getKing().setPosition(new Position(0, 4));
	  // ... similarly for other white pieces	
	
	  this.board[7][1] = black.getKnights(0);
	  black.getKnight(0).setPosition(new Position(7, 1));
	  this.board[7][6] = black.getKnights(1);
	  black.getKnight(1).setPosition(new Position(7, 6));
	  this.board[7][3] = black.getQueen();
	  black.getQueen().setPosition(new Position(7, 3));
	  this.board[7][4] = black.getKing();
	  black.getKing().setPosition(new Position(7, 4));
	  // ... similarly for other black pieces
     }
	
     public Piece getPiece(Position pos) {
	  return board[pos.x][pos.y];
     }
	
     public void setPiece(Piece piece, Position pos) {
	  this.board[pos.x][pos.y] = piece;
     }
}
```

# ChessGame
```java
public class ChessGame {
     private Player black;
     private Player white;
     private ChessBoard chessBoard;
     private boolean whiteTurn;
     private GameStatus status;
	
     public ChessGame() {
	this.black = new Player(false);
	this.white = new Player(true);
	this.chessBoard = new ChessBoard(black, white);	
	this.whiteTurn = true;
	this.status = GameStatus.ACTIVE;
    }
}    
```

# References :
1. https://github.com/MayV/ChessGame
2. https://www.youtube.com/watch?v=9soBz9lhZek

