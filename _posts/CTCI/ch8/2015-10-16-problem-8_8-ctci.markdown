---
layout: post
title: "Problem 8_8[CTCI]"
modified:
categories: /ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-10-16T15:58:24-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_8)

###Q:
Othello is played as follows: Each Othello piece is white on one side and black on the other. When a piece is surrounded by its opponents on both the left and right sides, or both the top and bottom, it is said to be captured and its color is flipped. On your turn, you must capture at least one of your opponent's pieces. The game ends when either user has no more valid moves. The win is assigned to the person with the most pieces. Implement the object-oriented design for Othello.

###A:
Well initially, this makes me think about the objects we will need.  We need some sort of board object.  I probably want to store that as a 2d array just for simplicity.  We will also need a piece object which has an attribute which allows for white and black pieces.  Players will probably also be necessary.

Some thoughts taken from the solutions:
- You might think to make a Piece object and then BlackPiece and WhitePiece which will inherit properties from Piece, but this is inadvisable since we will flip colors frequently.

- You may want to split up Game and Board, or you can keep it together.  I would keep it separate.

- Keeping score has different options.  I would probably do it in Board.

- It would help if Game was singleton class.  However, this is an assumption.

[Board.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_8/Board.java)

```java
public class Board
{
	private int blackCount = 0;
	private int whiteCount = 0;
	//2d array to represent the pieces
	private Piece[][] board;

	public Board(int rows, int columns)
	{
		board = new Piece[rows][columns];
	}

	public void initialize()
	{
		int middleR = board.length/2;
		int middleC = board[middleR].length/2;
		board[middleR][middleC] = new Piece(Color.White);
		board[middleRow+1][middleC] = new Piece(Color.Black);
		board[middleRow+1][middleC+1] = new Piece(Color.White);
		board[middleRow][middleC+1] = new Piece(Color.White);
		blackCount = 2;
		whiteCount = 2;
	}

	public boolean placeColor(int row, int column, Color c)
	{
		if (board[row][column] != null)
		{
			return false;
		}
		else
		{
			//For directions to flip
			int[] results = new int[4];
			results[0] = flipSection(row-1,column,color,Direction.up);
			results[1] = flipSection(row+1,column,color,Direction.down);
			results[2] = flipSection(row,column+1,color,Direction.right);
			results[3] = flipSection(row,column-1,color,Direction.left);
			
			int flipped = 0;
			for (int i = 0; i< 4;i++)
			{
				if (results[i] > 0)
				{
					flipped +=results[i];
				}
			}

			if(flipped <=0)
			{
				return false;
			}

			piece[row][column] = new Piece(c);
			updateScore(c, flipped+1);
		}
			return true;
	}
	public int flipSection(int row, int column, Color color, Direction d)
	{
		int r=0;
		int c=0;
		switch(d)
		{
		case up:
			r = -1;
			break;
		case down:
			r = 1;
			break;
		case left:
			c = -1;
			break;
		case right:
			c = 1;
			break;
		}
		if(row < 0|| column < 0 || row > board.length|| column > board[row].length || board[row][column] == null)
		{
			return -1;
		}

		if(board[row][column].getColor() == color)
		{
			return 0;
		}
		int flipped = flipSection(row+r,colum + c, color, d)
		if(flipped <0)
		{
			return -1;
		}
		board[row][column].flip();
		return flipped +1;
	}
	public int getScoreForColor(Color c)
	{
		if(c == Color.Black)
		{
			return blackCount;
		}
		return whiteCount;
	}
	public void updateScore(Color c, int news)
	{
		if(c == Color.Black)
		{
			whiteCount -= (news-1);
			blackCount += news;
		}
		else
		{
			whitecount +=news;
			blackCount -=(news-1);
		}
	}
	public void printBoard()
	{
		for(int row =0; row< board.length;row++)
		{
			for (int column = 0; column < board[row].length;i++)
			{
				if(board[row][column] == null)
				{
					System.out.print("_");
				}
				else if(board[row][column] == Color.Black)
				{
					System.out.print("B");
				}
				else if (board[row][column] == Color.White)
				{
					System.out.print("W");
				}
			}
			System.out.println();
		}
	}
}
```

[Color.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_8/Color.java)

```java
public enum Color
{
	White, Black;
}
```

[Game.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_8/Game.java)

```java
public class Game
{
	//This will be sized at 2
	private Player[] players;
	private static Game _instance;
	private Board board;
	//We create this as a singleton.  Also we assume 10x10
	private final int ROWS = 10;
	private final int COLUMNS = 10;

	private Game()
	{
		board = new Board(ROWS,COLUMNS);
		players = new Player[2];
		players[0] = new Player(Color.Black);
		players[1] = new Player(Color.White);
	}
	//Standard singleton stuff.
	public static Game getInstance()
	{
		if(_instance == null)
		{
			_instance = new Game();
		}
		return _instance;
	}
	public Board getBoard()
	{
		return board;
	}
}
```

[Piece.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_8/Piece.java)

```java
public class Piece
{
	private Color color;
	public Piece(Color c)
	{
		color = c;
	}
	//Flip the color
	public void flip()
	{
		if(color == Color.White)
		{
			color = Color.Black;
		}
		else
		{
			color = Color.White;
		}
	}
	public Color getColor()
	{
		return color;
	}
}
```

[Piece.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_8/Piece.java)

```java
public class Player
{
	private Color color;
	public Player(Color c)
	{
		color = c;
	}
	public int getScore()
	{
		return Game.getInstance().getBoard().getScoreForColor(color);
	}

	public boolean movePiece(int row, int column)
	{
		return Game.getInstance().getBoard().placeColor(row,column,color);
	}

	public Color getColor()
	{
		return color;
	}
}
```


