# Java-WordGolf-Practice-Unrefined
# This code is used to make the game Word Golf
# Current Issue: getDistanceFrom() is not working properly
import java.util.Scanner;

class Hole {
	private int targetDistance;
	
	public Hole(){
		targetDistance = (int)(Math.random() * 51 + 50);
	}

	public int getDistance(){
		return this.targetDistance;
	}
}

class WordGolf {
	private Hole h1;
	private Hole h2;
	private int strokes;
	private String sentence;
	private int yardage;
	private int distanceFrom;

	public WordGolf(){
		strokes = 1;
		sentence = "";
		yardage = 0;
		h1 = new Hole();
		h2 = new Hole();
		distanceFrom = h1.getDistance();
	}

	public void startGame(){
		Scanner kb = new Scanner(System.in);

		System.out.println("Welcome to WordGolf! Your course has 2 holes.");
		System.out.println("Hole #1 requires " + h1.getDistance() + " yards to make the hole");
		System.out.println("Hole #2 requires " + h2.getDistance() + " yards to make the hole");
		System.out.println();

		System.out.println("Welcome to hole #1. Your target is " + h1.getDistance() + " yards away.");
		while(getDistanceFrom(h1) != 0){
			System.out.print("Enter your sentence (stroke #" + strokes + "): ");
			sentence = kb.nextLine();
			yardage += computeYardage();
			System.out.println("Stroke #" + this.strokes + ": " + sentence + " is worth " + computeYardage() + " yards");
			this.strokes++;
			System.out.println("Total distance so far: " + yardage + ". You are " + getDistanceFrom(h1) + " from the target.");
		}
	}

	public int computeYardage(){
		int numSpaces = 0;
		String str = "";
		int result = 0;
		String sen = sentence;

		for(int i = 0; i < sen.length();i++){
			if(sen.charAt(i) == ' '){
				numSpaces++;
			}
		}

		if(numSpaces >= 4){
			return 0;
		}

		while(sen.length() > 0){
			if(sen.indexOf(" ") != -1) { 
				str = sen.substring(0,sen.indexOf(" "));
			} else {
				str = sen;
			}
			int total = 1;
			for(int i = 0;i<str.length();i++){
				if(str.charAt(i) == 'a' || str.charAt(i) == 'e' || str.charAt(i) == 'i' || str.charAt(i) == 'o' || str.charAt(i) == 'u'){
					total *= 2;
				} else {
					total += 1;
				}
			}
			result += total;
			if(sen.indexOf(" ") >= 0){
				sen = sen.substring(sen.indexOf(" ") + 1);
			} else {
				sen = "";	
			}
		}

		return result;
	}

	public int getYardage(){
		return this.yardage;
	}

	public int getDistanceFrom(Hole h){
		if(distanceFrom - computeYardage() > 0)	
			distanceFrom -= computeYardage();
		else
			distanceFrom += computeYardage();
		return distanceFrom;
	}
}

public class WordTester {
	public static void main(String[] args){
		WordGolf game1 = new WordGolf();

		game1.startGame();
	}
}
