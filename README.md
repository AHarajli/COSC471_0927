# COSC471_0927
/*Alaa Harajli
 * (0927)
 * This program writes to a random access file and reads from it
 * the methods we use are writeRecordToFile for writeing a record to the file
 * readRandomFile for reading the record
 * FindDoubleRecord for outputing the doublfeilds each on a seprate line
 * FindRecord which locates the record based on the int given
 * printChars which will print out the chars based on the int given 
 * 
 */

import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.util.Scanner;

public class driver {
	public static String file = "471randomacfile.txt";
	public static Scanner input = new Scanner(System.in);

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		try {

			writeRecordToFile(file, 1, 1.0, 'a');
			readRandomfile(file, 0, 0);
			writeRecordToFile(file, 2, 2.0, 'b');
			readRandomfile(file, 14, 0);
			writeRecordToFile(file, 3, 3.0, 'c');
			readRandomfile(file, 28, 0);
			writeRecordToFile(file, 4, 4.0, 'd');
			readRandomfile(file, 42, 0);
			writeRecordToFile(file, 5, 5.0, 'e');
			readRandomfile(file, 56, 0);
			writeRecordToFile(file, 6, 6.0, 'f');
			readRandomfile(file, 70, 0);
			findDoubleRecord(file);
			findRecord(file);
			printChars(file);
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}

	public static void printChars(String File) throws IOException {
		RandomAccessFile rfile = new RandomAccessFile(file, "rw");

		System.out.println(
				"Enter a interger value between 2 and 5 and you will recive a char for every record less than and equal to the value");
		int recordsSelected = input.nextInt();
		int bytesOfRecords = recordsSelected * 14;
		int postion = 14 - 2;
		while (postion <= bytesOfRecords) {
			rfile.seek(postion);
			postion += 14;
			System.out.println(" " + rfile.readChar());
		}
	}

	public static void findRecord(String File) throws IOException {
		RandomAccessFile rfile = new RandomAccessFile(file, "rw");
		int size = (int) rfile.length();
		int amountOfRecords = size / 14;

		System.out.println("Select a record you wish to print out. There are " + amountOfRecords + " Records");
		int RecordSelected = input.nextInt();
		int FindRecord = (RecordSelected * 14) - 14;

		rfile.seek(FindRecord);
		System.out.println("" + rfile.readInt() + " " + rfile.readDouble() + " " + rfile.readChar());

	}

	public static void findDoubleRecord(String File) throws IOException {
		RandomAccessFile rfile = new RandomAccessFile(file, "rw");

		int postionOfDoubles = 4;
		rfile.seek(postionOfDoubles);
		for (int rec = 0; rec < rfile.length(); rec++) {
			System.out.println("" + rfile.readDouble());
			if (postionOfDoubles >= rfile.length() - 10) {
				break;
			}
			if (postionOfDoubles < rfile.length()) {
				rfile.seek(postionOfDoubles += 14);
			}

		}

	}

	public static void readRandomfile(String file, int pos, int size) throws IOException {
		RandomAccessFile rfile = new RandomAccessFile(file, "rw");
		rfile.seek(pos);

		System.out.println("" + rfile.readInt() + ", " + rfile.readDouble() + ", " + rfile.readChar());

	}

	public static void writeRecordToFile(String file, int value, double Dvalue, char Cvalue) throws IOException {
		RandomAccessFile rfile = new RandomAccessFile(file, "rw");
		rfile.seek((int) rfile.length());
		rfile.writeInt(value);
		rfile.writeDouble(Dvalue);
		rfile.writeChar(Cvalue);

		rfile.close();
	}

}
