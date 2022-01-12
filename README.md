# Design a chess game

## System requirements :

1. Till the game is ACTIVE, players have to take their turn.

2. In each turn, take move input from the user and if the move is valid, allow move.

3. Continue the game until a player wins the game or the game is a draw. (Consider only CheckMate and StaleMate condition)

4. Handle Check conditions.


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

