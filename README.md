# vending-mashine

import java.math.BigDecimal;
import java.math.RoundingMode;

public class VendingMachine {
	
	private double currentBalance = 0;
	private double totalCoinsInserted = 0;
	private double totalMoneyCollected = 0;
	private int numberOfDrinksAvailable = 20;
	private int numberOfSweetsAvailable = 20;
	
	public VendingMachine() {
	}
	
	public VendingMachine(int startingDrinks, int startingSweets) {
		this.numberOfDrinksAvailable = startingDrinks;
		this.numberOfSweetsAvailable = startingSweets;
	}
	
	public void insertMoney(double amountOfMoney) {
		if (amountOfMoney >= 0) {
			totalCoinsInserted += amountOfMoney;
		}
		else {
			System.out.println("You can't con this machine!");
		}
	}
	
	public BigDecimal getMoneyLeft() {
		BigDecimal moneyLeft = new BigDecimal(totalCoinsInserted);
		return moneyLeft.setScale(2, RoundingMode.HALF_UP);
	}
	
	private void returnChange() {
		BigDecimal change = new BigDecimal(totalCoinsInserted);
		if (totalCoinsInserted > 0) {
			System.out.println("You get £" + change.setScale(2, RoundingMode.HALF_UP) + " change back!");
			totalCoinsInserted-=totalCoinsInserted;
		}
	}
	
	public void buyDrink() {
		if (totalCoinsInserted >= 0.7 && numberOfDrinksAvailable > 0) {
			totalCoinsInserted -= 0.7;
			currentBalance += 0.7;
			System.out.println("You buy a drink!");
		}
		else {
			System.out.println("You either haven't inserted enough money or there aren't any drinks left!");
		}
	}
	
	public void buySweet() {
		if (totalCoinsInserted >= 0.5 && numberOfSweetsAvailable > 0) {
			totalCoinsInserted -= 0.5;
			currentBalance += 0.5;
			System.out.println("You buy a sweet!");
		}
		else {
			System.out.println("You either haven't inserted enough money or there aren't any sweets left!");
		}
	}
	
	public void finish() {
		returnChange();
	}

	public static void main(String[] args) {
		VendingMachine test = new VendingMachine(25, 25);
		
		test.insertMoney(1);
		
		for (int i=0; i<3; i++) {
			test.buyDrink();
			test.buySweet();
			System.out.println("You have £" + test.getMoneyLeft() + " left.");
		}
		
		test.finish();
	}

}
