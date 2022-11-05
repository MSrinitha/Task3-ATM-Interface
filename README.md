# Task3-ATM-Interface


import java.awt.*;

import javax.swing.*;

import java.awt.event.*;

import java.io.*;

import java.util.*;

public class ATM {

public static void main(String[] args) {

BankAccount ba = new BankAccount("Krishna", "7593");

ba.login();

}

}

class BankAccount extends JFrame {

int balance;

int withdraw;

int deposit;

int prevTransaction;

String userName;

String userId;

int flag = 0;

JRadioButton jRadioButton1;

JRadioButton jRadioButton2;

JRadioButton jRadioButton3;

JRadioButton jRadioButton4;

JRadioButton jRadioButton5;

JRadioButton jRadioButton6;

	JButton jButton;

	ButtonGroup G1;

	JLabel L1;
    BankAccount(String uName, String uId) {
 
       userName = uName;
	   userId = uId;
    }
	void login() {
        System.out.println("Welcome "+ userName);
        System.out.println();
        System.out.print("ENTER PIN ");
        Scanner sc = new Scanner(System.in);
        String chkid = sc.nextLine();

        if (chkid.equals(userId)) {
            
            BankAccount f=new BankAccount();
			f.setBounds(200, 200, 500, 500);
			f.setTitle("Atm");
			f.setVisible(true);
        } else {
            System.out.println("-------------------------------");
            System.out.println("Invalid Login!!");
            System.out.println("-------------------------------");

            if (flag < 3) {
                flag++;
                login();
            }
        }
    }

	public BankAccount()
	{

		
		this.setLayout(null);

		jRadioButton1 = new JRadioButton();
		jRadioButton2 = new JRadioButton();
		jRadioButton3 = new JRadioButton();
		jRadioButton4 = new JRadioButton();
		jRadioButton5 = new JRadioButton();
		jRadioButton6 = new JRadioButton();

		
		jButton = new JButton("Enter");

		
		G1 = new ButtonGroup();

		
		L1 = new JLabel("Select an option:");

	
		jRadioButton1.setText("Withdraw");
		jRadioButton2.setText("Deposit");
		jRadioButton3.setText("Balance");
		jRadioButton4.setText("Quit");
		jRadioButton5.setText("Transfer");
		jRadioButton6.setText("Transaction History");

		// Setting Bounds
		jRadioButton1.setBounds(120, 40, 120, 50);
		jRadioButton2.setBounds(270, 40, 80, 50);
		jRadioButton3.setBounds(120, 70, 120, 50);
		jRadioButton5.setBounds(270, 70, 80, 50);
		jRadioButton6.setBounds(120, 100, 200, 50);
		jRadioButton4.setBounds(120, 130, 80, 50);


		
		jButton.setBounds(170, 200, 80, 30);

		
		L1.setBounds(20, 10, 200, 50);

		
		this.add(jRadioButton1);
		this.add(jRadioButton2);
		this.add(jRadioButton3);
		this.add(jRadioButton4);
		this.add(jRadioButton5);
		this.add(jRadioButton6);

		
		this.add(jButton);

		
		this.add(L1);

		G1.add(jRadioButton1);
		G1.add(jRadioButton2);
		G1.add(jRadioButton3);
		G1.add(jRadioButton4);
		G1.add(jRadioButton5);
		G1.add(jRadioButton6);

		
		jButton.addActionListener(new ActionListener() {
			
			public void actionPerformed(ActionEvent e)
			{
				
				if (jRadioButton1.isSelected()) {
				String input;
				input=JOptionPane.showInputDialog("Enter money to be withdrawn:");
				withdraw=Integer.parseInt(input);
                		if(balance >= withdraw)
                		  {
                    		  balance = balance - withdraw;
				  prevTransaction = -withdraw;
                    		  JOptionPane.showMessageDialog(BankAccount.this, "Please collect your Money");
                		  }
                		else
                		{
                    		JOptionPane.showMessageDialog(BankAccount.this,"Insufficient Balance");
                		}
			      }

				else if (jRadioButton2.isSelected()) {
					String input;
					input=JOptionPane.showInputDialog("Enter money to be deposited:");
					deposit=Integer.parseInt(input);
            				balance = balance + deposit;
					prevTransaction=deposit;
            				JOptionPane.showMessageDialog(BankAccount.this,"Your Money has been successfully deposited");
				}
				
				else if (jRadioButton3.isSelected()) {

					JOptionPane.showMessageDialog(BankAccount.this,"Balance="+balance);
				}
				else if (jRadioButton4.isSelected()) {

					System.exit(0);
				}
				else if(jRadioButton5.isSelected()){
				
				BankAccount bb = new BankAccount("Shiva", "3187");
                   		String input;
				input=JOptionPane.showInputDialog("Enter Amount to be Transfer:");
				int am=Integer.parseInt(input);
                   		if (balance < am) {
            			  JOptionPane.showMessageDialog(BankAccount.this,"Transfer Fails due to insufficient balance!");
                   		} 
				else {
            			balance -= am;
            			bb.balance += am;
            			JOptionPane.showMessageDialog(BankAccount.this,"Your Account becomes $" + balance);
				JOptionPane.showMessageDialog(BankAccount.this,"Account of " + bb.userName + " becomes $" + bb.balance);
            
                  		}
				}
				else if(jRadioButton6.isSelected()){
					if (prevTransaction > 0) {
            				JOptionPane.showMessageDialog(BankAccount.this,"Deposited: " + prevTransaction);
        			} 
					else if (prevTransaction < 0) {
            				JOptionPane.showMessageDialog(BankAccount.this,"Withdraw: " + Math.abs(prevTransaction));
        			} 
					else {
            				JOptionPane.showMessageDialog(BankAccount.this,"No Transaction Occured ");
        			}
				}
				else {

					JOptionPane.showMessageDialog(BankAccount.this,"NO Button selected");
				}

				
			}
		});
		 
	}

	
}//BankAccount
