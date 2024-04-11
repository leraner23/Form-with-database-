# Form-with-database-
Form made with the java Swing and the postgres sql database and server  




//// Codes : 



// import packages

import javax.swing.*;
import java.awt.event.*;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class form2 {

// Url , user , password for connection establishment 

	public static String url = "jdbc:postgresql://localhost:5432/Form";
	public static String user = "postgres";
	public static String password = "***";

 
 // table name 
 
	public static String tablename = "form";

 
 // text area 
 
	public static JTextArea h3 = new JTextArea();


// method for selections of Favourite food  

     public static String Foods(boolean Pizza, boolean Momo, boolean Cheese, boolean Burger, boolean Noodles) {
		StringBuilder sb = new StringBuilder();
		if (Pizza) {
			sb.append("Pizza, ");
		}
		if (Momo) {
			sb.append("Momo, ");
		}
		if (Cheese) {
			sb.append("Cheese, ");
		}
		if (Noodles) {
			sb.append("Noodles, ");
		}
		if (Burger) {
			sb.append("Burger, ");
		}
		return sb.toString();
	}

// method to insert data in table 

	public void insertTable(String roll, String name, String college_name, String gender, String fav_food) {
		try (Connection c = DriverManager.getConnection(url, user, password); Statement s = c.createStatement()) {
			String i = String.format(
					"INSERT INTO form(roll,name,college_name,gender,fav_food) VALUES ('%s','%s','%s','%s','%s')", roll,
					name, college_name, gender, fav_food);
			System.out.println(i);
			s.executeUpdate(i);
       System.out.println(" data inseted");
		} catch (Exception e) {
			System.out.println(e + "execption");
		}

	}

//method to update the data in the table 

	public void updateTable(String roll, String name, String college_name, String gender, String fav_food) {
		try (Connection c = DriverManager.getConnection(url, user, password); Statement s11 = c.createStatement()) {
			String Update11 = String.format(
					"UPDATE form  SET name = '%s', college_name = '%s', gender = '%s', fav_food ='%s'  WHERE roll= '%s'",
					name, college_name, gender, fav_food, roll);
			s11.executeUpdate(Update11);
			System.out.println("data is updated");
		} catch (Exception e) {
			System.out.println(e + "execption");
		}

	}


// method to delete the data from the table 

	public void deleteData(String roll) {
		try (Connection c = DriverManager.getConnection(url, user, password); Statement s = c.createStatement()) {
			String delete11 = String.format("DELETE FROM Form Where roll= %s", roll);
			s.executeUpdate(delete11);
			System.out.println("data is deleted");

		} catch (Exception e) {
			System.out.println(e + "execption");
		}

	}

// method to show single data in text area 

	public void showData(String roll) {
		try (Connection c = DriverManager.getConnection(url, user, password); Statement s = c.createStatement()) {
			String select1 = String.format("SELECT * FROM form WHERE roll = '%s' ORDER BY roll ASC", roll);
			ResultSet rs = s.executeQuery(select1);
			while (rs.next()) {
				String roll1 = rs.getString("roll");
				String name1 = rs.getString("name");
				String collegeName1 = rs.getString("college_name");
				String gender1 = rs.getString("gender");
				String favoritef1 = rs.getString("fav_food");

// to show in consloe 

				System.out.println(roll1);
				System.out.println(name1);
				System.out.println(collegeName1);
				System.out.println(gender1);
				System.out.println(favoritef1);

// to show in text area 

				h3.append( "\t" + "  Roll : " + roll1 + "\n");
				h3.append( "\n" + "  Name : " + name1 + "\n");
				h3.append( "\n" + "  College Name : " + collegeName1 + "\n");
				h3.append("\n" + "  Gender : " + gender1 + "\n");
				h3.append( "\n" + "  Favorite food : " + favoritef1 + "\n" + "\n" + "\n" );

			}
		} catch (Exception e) {
			System.out.println(e + "execption");
		}

	}

 // method to show all the  data  of database in text area
 
	public void showAllData(String roll) {
		try (Connection c = DriverManager.getConnection(url, user, password); Statement s = c.createStatement()) {
			String select1 = String.format("SELECT * FROM form ORDER BY roll ASC");
			ResultSet rs = s.executeQuery(select1);
			while (rs.next()) {
				String roll1 = rs.getString("roll");
				String name1 = rs.getString("name");
				String collegeName1 = rs.getString("college_name");
				String gender1 = rs.getString("gender");
				String favoritef1 = rs.getString("fav_food");

// to show in consloe 

				System.out.println(roll1);
				System.out.println(name1);
				System.out.println(collegeName1);
				System.out.println(gender1);
				System.out.println(favoritef1);

    
// to show in text area 

				h3.append( "\t" + "  Roll : " + roll1 + "\n");
				h3.append( "\n" + "  Name : " + name1 + "\n");
				h3.append( "\n" + "  College Name : " + collegeName1 + "\n");
				h3.append("\n" + "  Gender : " + gender1 + "\n");
				h3.append( "\n" + "  Favorite food : " + favoritef1 + "\n" + "\n" + "\n" );
			}
		} catch (Exception e) {
			System.out.println(e + "execption");
		}

	}

 
// main class 


	public static void main(String[] args) {

// frame

		JFrame j = new JFrame("Form array List :");

  // default close operation 
  
		j.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

// roll 

     JLabel roll = new JLabel("Roll :");
		roll.setBounds(20, 10, 100, 30);   // to give the position of the label in the frame
		j.add(roll);   // to add roll in Jframe

  // roll's textfield
  
		JTextField h = new JTextField();
		h.setBounds(20, 40, 180, 30);
		j.add(h);

// name

		JLabel name = new JLabel("Name :");
		name.setBounds(20, 80, 100, 30);  // to give the position of the label in the frame
		j.add(name);
  
   // name's textfield
   
		JTextField h1 = new JTextField();
		h1.setBounds(20, 110, 180, 30);
		j.add(h1);  

// college name 

		JLabel cname = new JLabel("College Name :");
		cname.setBounds(20, 150, 100, 30);
		j.add(cname);
    
   // college name's textfield
   
		JTextField h2 = new JTextField();
		h2.setBounds(20, 180, 180, 30);
		j.add(h2);

// gender

		JLabel gender = new JLabel("Gender :");
		gender.setBounds(20, 220, 100, 30);
		j.add(gender);

  // to show radio button 
  
		JRadioButton male = new JRadioButton("Male");
		JRadioButton female = new JRadioButton("Female");

  // to make only one to choose
  
		ButtonGroup group = new ButtonGroup();
		group.add(male);
		group.add(female);
		j.add(male);
		j.add(female);
		male.setBounds(20, 260, 100, 30);
		female.setBounds(130, 260, 100, 30);
  
// favourite foods 

		JLabel Ff = new JLabel("Favorite Foods :");
		Ff.setBounds(20, 300, 100, 30);
		j.add(Ff);

  // to show checkbox button
  
		JCheckBox f1 = new JCheckBox("Pizza");
		JCheckBox f2 = new JCheckBox("Burger");
		JCheckBox f3 = new JCheckBox("Cheese");
		JCheckBox f4 = new JCheckBox("MOMO");
		JCheckBox f5 = new JCheckBox("Noodles");
		j.add(f1);  
		j.add(f2);
		j.add(f3);
		j.add(f4);
		j.add(f5);
		f1.setBounds(20, 330, 110, 30);
		f2.setBounds(20, 360, 110, 30);
		f3.setBounds(20, 390, 110, 30);
		f4.setBounds(20, 420, 110, 30);
		f5.setBounds(20, 450, 110, 30);


// to show the data 

		JLabel AA = new JLabel("List of Students :");
		AA.setBounds(440, 10, 100, 30);
		j.add(AA);

		j.add(h3);
		h3.setBounds(420, 40, 280, 600);


 // to make scroll panel in the text area
 
		JScrollPane ss = new JScrollPane(h3);
		j.add(ss);
		ss.setBounds(440, 40, 280, 600);

// to make submit button

		JButton b = new JButton("Submit");
		j.add(b);
		b.setBounds(130, 500, 110, 30);

// action listener of submit button  
// this helps to make the button work 

		b.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {

				String roll = h.getText();

				String name = h1.getText();

				String college = h2.getText();

				String gender = "";
				if (male.isSelected()) {
					gender = "male";
				} else if (female.isSelected()) {
					gender = "female";
				}

				String favouriteFoods = Foods(f1.isSelected(), f4.isSelected(), f2.isSelected(), f3.isSelected(),
						f5.isSelected());

 // object of form2
      
				form2 obj = new form2();

    
// to apply insert method

				obj.insertTable(roll, name, college, gender, favouriteFoods);
			}
		});


// show all button

		JButton sa = new JButton("Show all");
		j.add(sa);
		sa.setBounds(260, 500, 110, 30);

// action listener of show all  button

		sa.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {

				String roll = h.getText();

				form2 obj = new form2();

//    to set the text area null / clear before adding the new data 

			h3.setText(null);
				obj.showAllData(roll);

			}
		});
		
		
// to enter roll number to check 
		
		JLabel select = new JLabel("Enter Roll no. :");
		select.setBounds(20, 550, 100, 30);
		j.add(select);
		JTextField h6 = new JTextField();
		h6.setBounds(20, 580, 150, 30);
		j.add(h6);

		JButton se = new JButton("Show");
		j.add(se);
		se.setBounds(180, 580, 110, 30);

		se.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {

				String roll = h6.getText();

				form2 obj = new form2();
    
  //    to set the text area null / clear before adding the new data 

			h3.setText(null);
				obj.showData(roll);

			}
		});


// to update the data according to the enter roll 

		JButton u = new JButton("Update");
		j.add(u);
		u.setBounds(300, 580, 110, 30);

		u.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {

				String roll = h6.getText();

				String name = h1.getText();

				String college = h2.getText();

				String gender = "";
				if (male.isSelected()) {
					gender = "male";
				} else if (female.isSelected()) {
					gender = "female";
				}

				String favouriteFoods = Foods(f1.isSelected(), f4.isSelected(), f2.isSelected(), f3.isSelected(),
						f5.isSelected());
				form2 obj = new form2();

				obj.updateTable(roll, name, college, gender, favouriteFoods);
			}
		});



// to delete the data according to the enter roll 

		JButton d = new JButton("Delete");
		j.add(d);
		d.setBounds(240, 620, 110, 30);

		d.addActionListener(new ActionListener() {

			public void actionPerformed(ActionEvent e) {

				String roll = h.getText();
				form2 obj = new form2();

				obj.deleteData(roll);
			}
		});

  // to set size of Jframe
  
		j.setSize(750, 720);

  // to make no layout selected 
  
		j.setLayout(null);

  // to make JFrame visible 
  
		j.setVisible(true);
	}

}




output ===>



![Screenshot 2024-04-11 212643](https://github.com/leraner23/Form-with-database-/assets/160107123/3c0febf1-c12c-493e-85eb-010d4f67020f)
