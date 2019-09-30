# Java-project

package flight;
import javax.swing.JOptionPane;
import java.io.*;
import java.util.*;
import java.text.*;

public class flight
{
	    int selection;	
		int[] flight_number;
		String[] flight_city_origin;
		String[] flight_city_destination;
		String[] flight_date;
		String[] flight_time;
		int[] flight_seats;
		
		int[] reservation_code;
		int[] Rflight_number;
		String[] last_name;
		String[] first_name;
		String[] type_seats;
		double[] cost_seats;
		int rcount;
		int fcount;
		
	public  flight()
	{
	    
		flight_number= new int[100];
		flight_city_origin=new String[100];
		flight_city_destination=new String[100];
		flight_date=new String[100];
		flight_time=new String[100];
		flight_seats=new int[100];
		
		reservation_code=new int[100];
		Rflight_number= new int[100];
		last_name=new String[100];
		first_name=new String[100];
		type_seats=new String[100];
		cost_seats=new double[100];
		rcount=-1;
		fcount=-1;	
	}
   
	public  int read_flight()
	{
	    String newLine;
	    try 
		{
		BufferedReader flight_file = new BufferedReader(new FileReader("flightj.dat"));
		    		while ((newLine = flight_file.readLine()) !=null)
		    		{
		    			StringTokenizer delimiter = new StringTokenizer(newLine,"#");
		     			fcount=fcount+1;
		    			flight_number[fcount]= Integer.parseInt(delimiter.nextToken());
		    			flight_city_origin[fcount]=delimiter.nextToken();
		    			flight_city_destination[fcount]=delimiter.nextToken();
		    			flight_date[fcount]=delimiter.nextToken();
		    			flight_time[fcount]=delimiter.nextToken();
		    			flight_seats[fcount]=Integer.parseInt(delimiter.nextToken());
		    		} 
		    		flight_file.close();
		}
		catch (IOException error)
		{
			System.out.println("Error on file read"+error);
		}
		return fcount;
	}
	public void write_flight(int filter)
	{
		try 
		{
		BufferedWriter flight_file = new BufferedWriter(new FileWriter("flightj.dat"));
		    		for(int i=0; i<=fcount; i++)
		    		{	if(filter!=i)
		    			{
		    			String line=
		    			flight_number[i]+"#"+
		    			flight_city_origin[i]+"#"+
		    			flight_city_destination[i]+"#"+
		    			flight_date[i]+"#"+
		    			flight_time[i]+"#"+
		    			flight_seats[i];
		    			flight_file.write(line);
		    			flight_file.newLine();
		    			}
		    		}
		    		//reset array counts
		    		fcount=0;
		    		
		    		flight_file.close();
		}
		catch (IOException error)
		{
			System.out.println("Error on file read"+error);
		}
		
	}

	public void modify_flight()
	{
		int selection=0;
		 String output=("Modify Flight Information Menu\n")+
		 "1.	Add Flight\n"+
		 "2.	Delete Flight\n"+
		 "3.	Modify Flight\n"+
		 "4.	Exit this menu\n";
		 //option = in.nextInt();
	     String value=JOptionPane.showInputDialog(null,
		            output,"Input data",JOptionPane.QUESTION_MESSAGE);
		             selection= Integer.parseInt(value);
		            
		 if(selection==1)
		 {
			fcount=fcount+1;
 			flight_number[fcount]=
 			Integer.parseInt(JOptionPane.showInputDialog(null,
		            "Enter Flight Number:","Input data",JOptionPane.QUESTION_MESSAGE));
 			
 			flight_city_origin[fcount]=JOptionPane.showInputDialog(null,
		            "Enter flight city origin:","Input data",JOptionPane.QUESTION_MESSAGE);
 			flight_city_destination[fcount]=JOptionPane.showInputDialog(null,
		            "Enter flight city destination:","Input data",JOptionPane.QUESTION_MESSAGE);
 			flight_date[fcount]=JOptionPane.showInputDialog(null,
		            "Enter flight date:","Input data",JOptionPane.QUESTION_MESSAGE);
 			flight_time[fcount]=JOptionPane.showInputDialog(null,
		            "Enter flight time:","Input data",JOptionPane.QUESTION_MESSAGE);
 			flight_seats[fcount]=Integer.parseInt(JOptionPane.showInputDialog(null,
		            "Enter Flight seats:","Input data",JOptionPane.QUESTION_MESSAGE));
			 
		 }
		 if(selection==2)
		 {
			 String output1=display_flights();
			 if(output1.isEmpty())
			 { JOptionPane.showInputDialog(null,
				            "no flight exist","Input data",JOptionPane.QUESTION_MESSAGE);
			  
			 }
			 else
			 {
			int flight_num =Integer.parseInt(JOptionPane.showInputDialog(null,
			            output1,"Input data",JOptionPane.QUESTION_MESSAGE));
			
			 delete_flight(flight_num);
			 }
			 
		 }
		 if(selection==3)
		 {
			 String output1=display_flights();
			 if(output1.isEmpty())
			 { JOptionPane.showMessageDialog(null,
				            "no flight exist");
			  
			 }
			 else
			 {
			int flight_num =Integer.parseInt(JOptionPane.showInputDialog(null,
			            output1,"Input data",JOptionPane.QUESTION_MESSAGE));
				int index=-1;
				for(int i=0; i<=fcount; i++)
				{
					if(flight_number[i]==flight_num)
					{
						index=i;
						break;
					}
				}
				if(index!=-1)
				{
				 String modify=("Modify Flight Information of #"+flight_num+"\n")+
						 "1.	Edit flight city origin\n"+
						 "2.	Edit flight city destination\n"+
						 "3.	Edit flight date\n"+
						 "4.	Edit flight time\n"+
				 		 "5.	Edit flight seats\n";
				 
				 value=JOptionPane.showInputDialog(null,
						 modify,"Input data",JOptionPane.QUESTION_MESSAGE);
				             selection= Integer.parseInt(value);
				             
						 //option = in.nextInt();
				 while(selection<6 && selection>0) {
						   if(selection==1)
							   flight_city_origin[index]=JOptionPane.showInputDialog(null,
							            "Enter flight city origin:","Input data",JOptionPane.QUESTION_MESSAGE);
						   if(selection==2)	
						       flight_city_destination[index]=JOptionPane.showInputDialog(null,
							            "Enter flight city destination:","Input data",JOptionPane.QUESTION_MESSAGE);
						   if(selection==3)
					 			flight_date[index]=JOptionPane.showInputDialog(null,
							            "Enter flight date:","Input data",JOptionPane.QUESTION_MESSAGE);
						   if(selection==4)
					 			flight_time[index]=JOptionPane.showInputDialog(null,
							            "Enter flight time:","Input data",JOptionPane.QUESTION_MESSAGE);
						   if(selection==5)
					 			flight_seats[index]=Integer.parseInt(JOptionPane.showInputDialog(null,
							            "Enter Flight seats:","Input data",JOptionPane.QUESTION_MESSAGE));
						   
						   
						 value=JOptionPane.showInputDialog(null,
								 modify,"Input data",JOptionPane.QUESTION_MESSAGE);
							             selection= Integer.parseInt(value);
							          
				 }
						             
			 }
				else
					JOptionPane.showMessageDialog(null,"this flight number not exist");
			 }
					
		 }
		 if(selection==4)
		 {
			 return;
		 }
		 else
			 return;

	}
	public String display_flights()
	{  String output="";
	   output+="Flight Number | Origin | Destination | Date | Time | Seats"+"\n";
		for(int i=0; i<=fcount; i++)
		{
			 output+=
				            ""+flight_number[i]+
				            " | "+ flight_city_origin[i]+
				            " | "+flight_city_destination[i]+
				            " | "+flight_date[i]+
				            " | "+flight_time[i]+
				            " | "+flight_seats[i]
				            		+ "\n";
		}
		return output;
		
	}
	public void delete_flight(int flight_num) 
	{  
		int index=-1;
		for(int i=0; i<=fcount; i++)
		{
			if(flight_number[i]==flight_num)
			{
				index=i;
				break;
			}
		}
		if(index!=-1) {
		//write into file flightj.dat
			write_flight(index);
			// read flight
			fcount=read_flight();
		}
	}
	
	public void modify_reservation()
	{
		rcount=rcount+1;
		
		reservation_code[rcount]=Integer.parseInt(JOptionPane.showInputDialog(null,
			            "Enter reservation code :","Input data",JOptionPane.QUESTION_MESSAGE));
		Rflight_number[rcount]=Integer.parseInt(JOptionPane.showInputDialog(null,
			            "Enter reservation flight number:","Input data",JOptionPane.QUESTION_MESSAGE));
		first_name[rcount]=JOptionPane.showInputDialog(null,
	            "Enter Fisrt name:","Input data",JOptionPane.QUESTION_MESSAGE);
		last_name[rcount]=JOptionPane.showInputDialog(null,
			            "Enter Last Name:","Input data",JOptionPane.QUESTION_MESSAGE);
		type_seats[rcount]=JOptionPane.showInputDialog(null,
			            "Enter seat type:","Input data",JOptionPane.QUESTION_MESSAGE);
		cost_seats[rcount]=Double.parseDouble(JOptionPane.showInputDialog(null,
			            "Enter cost of seat:","Input data",JOptionPane.QUESTION_MESSAGE));
		return;
		
	}
	public void exit_program()
	{
		write_reservation();
		write_flight(-1);
		return;
	}

	public int menu()
	{
		int selection;
		String value,output="ACME Airlines"+"\n"+
	    "1.modify flight"+"\n"+
		"2.modify reservation"+"\n"+
		"3.Report section"+"\n"+
		"4. Exit"+"\n"+
		"Enter your selection>";
		
		value=JOptionPane.showInputDialog(null,
	            output,"Input data",JOptionPane.QUESTION_MESSAGE);
	             selection= Integer.parseInt(value);
	             
		return selection;
		
	
	}

	public  int read_reservation()
	{
		String newLine;
		//int selection;
	    try
	    
	    {
		BufferedReader reservation_file = new BufferedReader(new FileReader("reservationj.dat"));
		    		while ((newLine = reservation_file.readLine()) !=null)
		  {
		    	StringTokenizer delimiter= new StringTokenizer(newLine,"#");
		    	rcount=rcount+1;
				reservation_code[rcount]=Integer.parseInt(delimiter.nextToken());
				Rflight_number[rcount]=Integer.parseInt(delimiter.nextToken());
				last_name[rcount]= delimiter.nextToken();
				first_name[rcount]= delimiter.nextToken();
				type_seats[rcount]= delimiter.nextToken();
				cost_seats[rcount]=Double.parseDouble(delimiter.nextToken());
		  }
		    		reservation_file.close();
		    }
		    catch (IOException error)
		    {
		    	System.out.println("Error on file read"+error);
		    }
		    return rcount;
	}
	
	public void  write_reservation()
	{
	    try
	    
	    {
		BufferedWriter reservation_file = new BufferedWriter(new FileWriter("reservationj.dat"));
		  
		while(rcount>=0)
		  {
		    	
		    	
				String line=reservation_code[rcount]+"#"+
				Rflight_number[rcount]+"#"+
				last_name[rcount]+"#"+
				first_name[rcount]+"#"+
				type_seats[rcount]+"#"+
				cost_seats[rcount];
				reservation_file.write(line);
				reservation_file.newLine();
				rcount=rcount-1;
		  }
		    		reservation_file.close();
		    }
		    catch (IOException error)
		    {
		    	System.out.println("Error on file read"+error);
		    }
		   
	}

	public int find_reservation(int flight_numb){
		int reservation=0;
		
		for(int i=0; i<=rcount; i++)
		{
			if(Rflight_number[i]==flight_numb)
				reservation++;
		}
		return reservation;
	}
	public void report()
	{
		int selection,i;
		String value;
		//double total=0,average;
		String output="ACME Airlines"+"\n"+
	
		 "1.All flight Info"+"\n"+
		 "2.All Reservation Info"+"\n"+
		 "3.Value of reservation of a specific type"+"\n"+
		 "4.All Reservation on a specific flight"+"\n"+
		 "5.All flights from a specific city"+"\n"+
		 "6.Specific reservation information"+"\n"+
		 "7.Summary of all flights"+"\n"+
		 "8.Specific passenger flight detail"+"\n"+
		 "9.Exit Report Menu"+"\n"+
		 "please make your selection>";
			
			value=JOptionPane.showInputDialog(null,
		            output,"Input data",JOptionPane.QUESTION_MESSAGE);
		             selection= Integer.parseInt(value);
		             while(selection !=9)
		             {
		            	 if(selection ==1)
		            	 {
		            		 System.out.println("ALL FLIGHTS");
		            		 System.out.println("============");
		            		 for(i=0;i<=fcount;++i)
		            		 {
		            			 System.out.println(flight_number[i]+" "+flight_city_origin[i]+" "+flight_city_destination[i]+" "+flight_date[i]+" "+flight_time[i]+" "+flight_seats[i]);
		            		 }
		            	 }
		            	 //end of report 1
		            	else if(selection ==2)
		            	{
		            		 System.out.println("ALL reservations");
	                		 System.out.println("=================");
	            			 for(i=0;i<=rcount;++i)
	            			 {            			
	            					 System.out.println(reservation_code[i]+" "+Rflight_number[i]+" "+last_name[i]+" "+first_name[i]+" "+type_seats[i]+" "+cost_seats[i]);
	            				
	            			 }
	            		 }//end of report 2
		            	else if(selection ==3)
            			 {
            				 value=JOptionPane.showInputDialog(null,
             			            "Enter type seats to search for","Input data",JOptionPane.QUESTION_MESSAGE);
            				 System.out.println("All value Reservation of type");
            				 for(i=0;i<=rcount;++i)
            				 {
            					 if(value.equals(type_seats[i]))
            					 {
            						 System.out.println(reservation_code[i]+" "+Rflight_number[i]+" "+last_name[i]+" "+first_name[i]+" "+type_seats[i]+" "+cost_seats[i]);
            					 }
            				 }
            			 }//end of report 3
            			 else if(selection ==4)
            				 {
            					 value=JOptionPane.showInputDialog(null,
                  			            "Enter the flight number to search for","Input data",JOptionPane.QUESTION_MESSAGE);
            	                 int search_flight=Integer.parseInt(value);
                 				 System.out.println("All Reservations of this flight");
                 				 for(i=0;i<=rcount;++i)
                 				 {
                 					 if(search_flight==Rflight_number[i])
                 					 {
                 						 System.out.println(reservation_code[i]+" "+Rflight_number[i]+" "+last_name[i]+" "+first_name[i]+" "+type_seats[i]+" "+cost_seats[i]);
                 					 }
                 				 }
            		
            			}//end of report 4
		            				 
            			else if(selection ==5)
		            	{
            				String city =JOptionPane.showInputDialog("Enter the city to search for");
            				
            				System.out.println("Flight Number | Origin | Destination | Date | Time | Seats | Restervations"+"\n");
            				for(int j=0; j<=fcount; j++)
            				{
            					if(city.equals(flight_city_origin[j])==true) {
            						int reservation=find_reservation(flight_number[j]);
            						
            						System.out.print(""+flight_number[j]+
            						            " | "+ flight_city_origin[j]+
            						            " | "+flight_city_destination[j]+
            						            " | "+flight_date[j]+
            						            " | "+flight_time[j]+
            						            " | "+flight_seats[j]+
            						            " | "+reservation
            						            		+ "\n");
            					}
            				}
                            
		            	}			 //end of report 5
		            					 
            			else if(selection ==6) {
		             	  value =JOptionPane.showInputDialog("Enter the reservation code");
		                               int search=Integer.parseInt(value);
		            					 for(i=0;i<=rcount;++i)
		            					 {
		            						 if(search==reservation_code[i])
		            							 //System.out.println(reservation); 
		            							 for( int j=0;j<=fcount;++j)
		            							 {
		            								 if(flight_number[j]==Rflight_number[i])
		            									 {
		            									 
		            									 System.out.print("Flight: "+flight_number[j]+
		                     						            " | "+ flight_city_origin[j]+
		                     						            " | "+flight_city_destination[j]+
		                     						            " | "+flight_date[j]+
		                     						            " | "+flight_time[j]+
		                     						            " | "+flight_seats[j]+
		                     						            " "
		                     						            		+ "\n");
		            									 System.out.println("Reservation:" +
		            										reservation_code[i]+" | "+
		            										Rflight_number[i]+" | "+
		            										first_name[i]+" | "+
		            										last_name[i]+" | "+
		            										type_seats[i]+" | "+
		            										cost_seats[i]);
		            									 }
		            							 }
		            					 }
		                 }		                       						 
            			else if(selection ==7) {
						 for( int j=0;j<=fcount;++j)
						 {
							System.out.print(j+1+" Flight: "+flight_number[j]+
						            " | "+ flight_city_origin[j]+
						            " | "+flight_city_destination[j]+
						            " | "+flight_date[j]+
						            " | "+flight_time[j]+
						            " | "+flight_seats[j]+
						            " "
						            		+ "\n");
							for(i=0;i<=rcount;++i)
        					{
   								if(flight_number[j]==Rflight_number[i])
   								 {
   									 System.out.println("	Reservation:" +
   										reservation_code[i]+" | "+
   										Rflight_number[i]+" | "+
   										first_name[i]+" | "+
   										last_name[i]+" | "+
   										type_seats[i]+" | "+
   										cost_seats[i]);
   								 }
						 	}
							System.out.print("\n");
						 }
            			}
		                                     //end of report 7
            			else if(selection ==8) {
            				value =JOptionPane.showInputDialog("Enter the Passenger First Name");
                            
         					 for(i=0;i<=rcount;++i)
         					 {
         						 if(value.equals( first_name[i]))
         						 { 
         							 for( int j=0;j<=fcount;++j)
         							 {
         								 if(flight_number[j]==Rflight_number[i])
         									 {
         									 
         									 System.out.print("Flight: "+flight_number[j]+
                  						            " | "+ flight_city_origin[j]+
                  						            " | "+flight_city_destination[j]+
                  						            " | "+flight_date[j]+
                  						            " | "+flight_time[j]+
                  						            " | "+flight_seats[j]+
                  						            " "
                  						            		+ "\n");
         									 System.out.println("Reservation:" +
         										reservation_code[i]+" | "+
         										Rflight_number[i]+" | "+
         										first_name[i]+" | "+
         										last_name[i]+" | "+
         										type_seats[i]+" | "+
         										cost_seats[i]);
         									 }
         							 }
         						 }
         					 }
            			}
		            									 //end of report 8
		  				 
		            	  output="ACME Airlines"+"\n"+
		            				
						 "1.All flight Info"+"\n"+
						 "2.All Reservation Info"+"\n"+
						 "3.Value of reservation of a specific type"+"\n"+
						 "4.All Reservation on a specific flight"+"\n"+
						 "5.All flights from a specific city"+"\n"+
						 "6.Specific reservation information"+"\n"+
						 "7.Summary of all flights"+"\n"+
						 "8.Specific passenger flight detail"+"\n"+
						 "9.Exit Report Menu"+"\n"+
						 "please make your selection>";
		            						 
		            						 value=JOptionPane.showInputDialog(null,
		                     			           output,"Input data",JOptionPane.QUESTION_MESSAGE);
		                     			 selection=Integer.parseInt(value);
		            					
		             
		             }//end of while loop
		    }//end of report method
            	            				 
            					   					 		
      //all getter setter
	public int getSelection() {
		return selection;
	}
	public void setSelection(int selection) {
		this.selection = selection;
	}
	public int[] getFlight_number() {
		return flight_number;
	}
	public void setFlight_number(int[] flight_number) {
		this.flight_number = flight_number;
	}
	public String[] getFlight_city_origin() {
		return flight_city_origin;
	}
	public void setFlight_city_origin(String[] flight_city_origin) {
		this.flight_city_origin = flight_city_origin;
	}
	public String[] getFlight_city_destination() {
		return flight_city_destination;
	}
	public void setFlight_city_destination(String[] flight_city_destination) {
		this.flight_city_destination = flight_city_destination;
	}
	public String[] getFlight_date() {
		return flight_date;
	}
	public void setFlight_date(String[] flight_date) {
		this.flight_date = flight_date;
	}
	public String[] getFlight_time() {
		return flight_time;
	}
	public void setFlight_time(String[] flight_time) {
		this.flight_time = flight_time;
	}
	public int[] getFlight_seats() {
		return flight_seats;
	}
	public void setFlight_seats(int[] flight_seats) {
		this.flight_seats = flight_seats;
	}
	public int[] getReservation_code() {
		return reservation_code;
	}
	public void setReservation_code(int[] reservation_code) {
		this.reservation_code = reservation_code;
	}
	public int[] getRflight_number() {
		return Rflight_number;
	}
	public void setRflight_number(int[] rflight_number) {
		Rflight_number = rflight_number;
	}
	public String[] getLast_name() {
		return last_name;
	}
	public void setLast_name(String[] last_name) {
		this.last_name = last_name;
	}
	public String[] getFirst_name() {
		return first_name;
	}
	public void setFirst_name(String[] first_name) {
		this.first_name = first_name;
	}
	public double[] getCost_seats() {
		return cost_seats;
	}
	public void setCost_seats(double[] cost_seats) {
		this.cost_seats = cost_seats;
	}
	public int getRcount() {
		return rcount;
	}
	public void setRcount(int rcount) {
		this.rcount = rcount;
	}
	public int getFcount() {
		return fcount;
	}
	public void setFcount(int fcount) {
		this.fcount = fcount;
	}

	public static void main (String []args)
	{
		flight flight= new flight();
		flight.fcount=flight.read_flight();
		
		flight.rcount=flight.read_reservation();
		
		//String output,value;
		flight.selection= flight.menu();
		while (flight.selection !=4)
		{	
			if(flight.selection ==1)
				flight.modify_flight();
			else
				if(flight.selection ==2)
					flight.modify_reservation();
				else
					if(flight.selection ==3)
						flight.report();
					
	    flight.selection =flight.menu();
		}//end of while loop
		flight.exit_program();
		System.exit(0);
	}
} //end of main class
            			 
            			 
            		 
             
		 









