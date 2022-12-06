# Java-WordGolf-Practice-Unrefined
# This code is used to make the game Word Golf
#import java.util.Scanner;

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

	public WordGolf(){
		strokes = 1;
		sentence = "";
		yardage = 0;
		h1 = new Hole();
		h2 = new Hole();
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

		for(int i = 0; i < sentence.length();i++){
			if(sentence.charAt(i) == ' '){
				numSpaces++;
				//str = sentence.substring(0,i);
				//sentence = sentence.substring(i+1);
			}
		}

		if(numSpaces >= 4){
			return 0;
		}

		str = sentence.substring(0,sentence.indexOf(" "));
		while(sentence.length() > 0){
			int total = 1;
			for(int i = 0;i<str.length();i++){
				if(str.charAt(i) == 'a' || str.charAt(i) == 'e' || str.charAt(i) == 'i' || str.charAt(i) == 'o' || str.charAt(i) == 'u'){
					total *= 2;
				} else {
					total += 1;
				}
			}
			result = total;
			sentence = sentence.substring(sentence.indexOf(" ") + 1);
			
			if(sentence.indexOf(" ") > 0){
				str = sentence.substring(0,sentence.indexOf(" "));
			} else {
				str = ""; 
			}
		}

		return result;
	}

	public int getYardage(){
		return this.yardage;
	}

	public int getDistanceFrom(Hole h){
		return h.getDistance() - this.yardage;
	}
}

public class WordTester {
	public static void main(String[] args){
		WordGolf game1 = new WordGolf();

		game1.startGame();
	}
}
