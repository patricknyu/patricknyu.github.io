---
layout: post
title: "Problem 8_3[CTCI]"
modified:
categories: ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-09-28T12:43:14-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_3)

###Q:
Design a musical jukebox using object-oriented principles.

###A:
My initial thoughts are to make JukeBox and Song classes.

The JukeBox class would be the main class, which will have a array which holds all the songs.  Then there would be a play method which took in a string which described the song we wanted to play from the array, played it, and would consequently assign to a next song.  We would need a displayCurrentSong method as well.  We would need an AddToPlaylist method as well to add to a ArrayList of songs.

The Song class would have a song name, artist, year, and song length.  It would also have a play method where it would play the song.

I'll put in a rough outline.

[Jukebox.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_3/JukeBox.java)

```java
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

public class JukeBox
{
	//We assume that songs are built in and cannot be changed.

	private Song[] songs;  /*Songs go here*/
	public List<Song> playlist = new ArrayList<Song>();
	
	//Adds to list if it is not in songs.  This might have been better used as a hashset.
	public boolean AddToPlaylist(Song s)
	{
		if (!Arrays.asList(songs).contains(s))
		{
			return false;
		}
		else
		{
			playlist.add(s);
		}
		return true;
	}
	//Plays a certain # of songs
	public void play(int i)
	{
		//If there aren't enough songs in the playlist
		if (i >playlist.size())
		{
			System.out.println("TOO LONG");
		}
		while (i > 0)
		{
			playlist.get(0).play();
			playlist.remove(0);
		}
	}
}
```

[Song.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_3/Song.java)

```java
public class Song
{
	private int year;
	private String artist;
	private String lyrics;
	private int length;
	private String name;
	
	public Song(String n, String a, String lyr, int len, int y)
	{
		name = n;
		artist = a;
		lyrics = lyr;
		length = len;
		year = y;
	}

	public void play()
	{
		System.out.println("Now Playing " + name + " by " + artist + " from " + year + ".");
		System.out.println(lyrics);
	}
}
```

