# Email_Fetcher
Space Cadets Challenge #1

import java.net.*;
import java.io.*;
import java.util.*;

public class Email_Fetcher {
	public static void main(String[] args) throws IOException {
		
		String siteLink = new String("https://www.ecs.soton.ac.uk/people/");
		System.out.println("Please enter the ID of the person you want to find");
		Scanner scanner = new Scanner(System.in); // This stores the email id of who you're looking for
		String emailID = scanner.nextLine();
		String fullLinkString = siteLink + emailID; //combines the id and the start of the link to create the link to the page of the person
		
		URL fullLink = new URL(fullLinkString);
		BufferedReader HTML = new BufferedReader(new InputStreamReader(fullLink.openStream())); // opens the link and stores the HTML source
		
		Boolean nameFound = false;
		String HTMLLine;
		while ((HTMLLine = HTML.readLine()) != null) { // reads each line at a time until it reaches the end
			if (HTMLLine.contains("property=\"name\"")) { // looks for "property="name"
				int nameIndexStart = HTMLLine.indexOf("property=\"name\""); // finds the index number before and after the name
				int nameIndexEnd = HTMLLine.indexOf("</h1>");
				System.out.print(HTMLLine.substring((nameIndexStart+16), nameIndexEnd)); // prints what is between the two index, which should be the name		
				nameFound = true;
				break;
			}
		}
		if (!nameFound) {
				System.out.println("No matching page found");
		}
		scanner.close();
		
	}
}
