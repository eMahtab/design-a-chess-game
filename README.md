# Design a chess game

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
		
	 for(int i=0;i<8;i++) {
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

