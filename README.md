# DataStructure

- [Practice I](#PracticeI)
	- [基础](#基础)
	- [Building a LinkedList class](#PartI)
	- [Merkle-Hellman Knapsack Cryptosystem](#PartII)
	- [Merkle tree](#PartIII)
- [Practice II](#PracticeII)
	- [基础](#基础)
	- [Queues and Red Black Trees](#Queues&RedBlackTrees)


### 基础
## PracticeI
This project has three objectives. First, the student will be introduced to the linked list data structure using Michael Main’s ObjectNode.java. Second, the student will use the linked list class created in Part 1 to implement Merkle-Hellman Knapsack cryptography. Third, the student will use the same linked list to build a Merkle Tree.

For more details, please look at the homework1 file.

### PartI
First, it is code for the tree node.
```
package edu.colorado.nodes;
// File: ObjectNode.java from the package edu.colorado.nodes
// Complete documentation is available from the ObjectNode link in:
//   http://www.cs.colorado.edu/~main/docs



/******************************************************************************
* A ObjectNode provides a node for a linked list with 
* Object data in each node.
*
* @note
*   Lists of nodes can be made of any length, limited only by the amount of
*   free memory in the heap. But beyond Integer.MAX_VALUE (2,147,483,647),
*   the answer from listLength is incorrect because of arithmetic
*   overflow. 
*
* @see
*   <A HREF="../../../../edu/colorado/nodes/ObjectNode.java">
*   Java Source Code for this class
*   (www.cs.colorado.edu/~main/edu/colorado/nodes/ObjectNode.java) </A>
*
* @author Michael Main 
*   <A HREF="mailto:main@colorado.edu"> (main@colorado.edu) </A>
*
* @version Feb 10, 2016
*
* @see Node
* @see BooleanNode
* @see CharNode
* @see DoubleNode
* @see FloatNode
* @see IntNode
* @see LongNode
* @see ShortNode
******************************************************************************/
public class ObjectNode
{
   // Invariant of the ObjectNode class:
   //   1. The node's Object data is in the instance variable data.
   //   2. For the final node of a list, the link part is null.
   //      Otherwise, the link part is a reference to the
   //      next node of the list.
   private Object data;
   private ObjectNode link;   


   /**
   * Initialize a node with a specified initial data and link to the next
   * node. Note that the initialLink may be the null reference, 
   * which indicates that the new node has nothing after it.
   * @param initialData
   *   the initial data of this new node
   * @param initialLink
   *   a reference to the node after this new node--this reference may be null
   *   to indicate that there is no node after this new node.
   * @postcondition
   *   This node contains the specified data and link to the next node.
   **/   
   public ObjectNode(Object initialData, ObjectNode initialLink)
   {
      data = initialData;
      link = initialLink;
   }


   /**
   * Modification method to add a new node after this node.   
   * @param item
   *   the data to place in the new node
   * @postcondition
   *   A new node has been created and placed after this node.
   *   The data for the new node is item. Any other nodes
   *   that used to be after this node are now after the new node.
   * @exception OutOfMemoryError
   *   Indicates that there is insufficient memory for a new 
   *   ObjectNode. 
   **/
   //O(1)
   //Ω(1)
   //θ(1)
   public void addNodeAfter(Object item)   
   {
      link = new ObjectNode(item, link);
   }          
   
   
   /**
   * Accessor method to get the data from this node.   
   * @return
   *   the data from this node
   **/
   //O(1)
   //Ω(1)
   //θ(1)
   public Object getData( )   
   {
      return data;
   }
   
   
   /**
   * Accessor method to get a reference to the next node after this node. 
   * @return
   *   a reference to the node after this node (or the null reference if there
   *   is nothing after this node)
   **/
   //O(1)
   //Ω(1)
   //θ(1)
   public ObjectNode getLink( )
   {
      return link;                                               
   } 
    
    
   /**
   * Copy a list.
   * @param source
   *   the head of a linked list that will be copied (which may be
   *   an empty list in where source is null)
   * @return
   *   The method has made a copy of the linked list starting at 
   *   source. The return value is the head reference for the
   *   copy. 
   * @exception OutOfMemoryError
   *   Indicates that there is insufficient memory for the new list.   
   **/ 
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(N)
   //θ(N)
   //precondition:the parameter called in the function should be a object node
   //and make sure we have enough memory space for the method
   public static ObjectNode listCopy(ObjectNode source)
   {
      ObjectNode copyHead;
      ObjectNode copyTail;
      
      // Handle the special case of the empty list.
      if (source == null)
         return null;
         
      // Make the first node for the newly created list.
      copyHead = new ObjectNode(source.data, null);
      copyTail = copyHead;
      
      // Make the rest of the nodes for the newly created list.
      while (source.link != null)
      {
         source = source.link;
         copyTail.addNodeAfter(source.data);
         copyTail = copyTail.link;
      }
 
      // Return the head reference for the new list.
      return copyHead;
   }
   
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(N)
   //θ(N)
   public static ObjectNode listCopy_rec(ObjectNode source)
   {
	   ObjectNode copyHead;
	   if (source==null)
		   return null;
	   
	   //base case
	   if (source.link==null) {
		   copyHead=new ObjectNode(source.data,null);
		   return copyHead;
	   }
	   //recursive case
	   else {
		   ObjectNode nextNode;
		   nextNode=listCopy_rec(source.link);
		   copyHead=new ObjectNode(source.data,nextNode);
		   return copyHead;
	   }
	   
   }
   
   
   /**
   * Copy a list, returning both a head and tail reference for the copy.
   * @param source
   *   the head of a linked list that will be copied (which may be
   *   an empty list in where source is null)
   * @return
   *   The method has made a copy of the linked list starting at 
   *   source.  The return value is an
   *   array where the [0] element is a head reference for the copy and the [1]
   *   element is a tail reference for the copy.
   * @exception OutOfMemoryError
   *   Indicates that there is insufficient memory for the new list.   
   **/
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(N)
   //θ(N)
   //precondition:the parameter called in the function should be a object node
   //and make sure we have enough memory space for the method
   public static ObjectNode[ ] listCopyWithTail(ObjectNode source)
   {
      ObjectNode copyHead;
      ObjectNode copyTail;
      ObjectNode[ ] answer = new ObjectNode[2];
     
      // Handle the special case of the empty list.   
      if (source == null)
         return answer; // The answer has two null references .
      
      // Make the first node for the newly created list.
      copyHead = new ObjectNode(source.data, null);
      copyTail = copyHead;
      
      // Make the rest of the nodes for the newly created list.
      while (source.link != null)
      {
         source = source.link;
         copyTail.addNodeAfter(source.data);
         copyTail = copyTail.link;
      }
      
      // Return the head and tail references.
      answer[0] = copyHead;
      answer[1] = copyTail;
      return answer;
   }
   
   
   /**
   * Compute the number of nodes in a linked list.
   * @param head
   *   the head reference for a linked list (which may be an empty list
   *   with a null head)
   * @return
   *   the number of nodes in the list with the given head 
   * @note
   *   A wrong answer occurs for lists longer than Int.MAX_VALUE.     
   **/   
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(N)
   //θ(N)
   public static int listLength(ObjectNode head)
   {
      ObjectNode cursor;
      int answer;
      
      answer = 0;
      for (cursor = head; cursor != null; cursor = cursor.link)
         answer++;
        
      return answer;
   }
   
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(N)
   //θ(N)
   public static int listLength_rec(ObjectNode head)
   {
	   int count=0;
	   if (head==null)
		   return count;
	 //base case
	   if (head.link==null) {
		   count=1;
		   return count;
	   }
	   //recursive case
	   else {
		   int lastCount=0;
		   lastCount=listLength_rec(head.link);
		   count=1+lastCount;
		   return count;
	   }
   }
   

   /**
   * Copy part of a list, providing a head and tail reference for the new copy. 
   * @precondition
   *   start and end are non-null references to nodes
   *   on the same linked list,
   *   with the start node at or before the end node. 
   * @return
   *   The method has made a copy of the part of a linked list, from the
   *   specified start node to the specified end node. The return value is an
   *   array where the [0] component is a head reference for the copy and the
   *   [1] component is a tail reference for the copy.
   * @param start
   *   first node to copy
   * @param end
   *   final node to copy
   * @exception IllegalArgumentException
   *   Indicates that start and end are not references
   *   to nodes on the same list.
   * @exception NullPointerException
   *   Indicates that start is null.
   * @exception OutOfMemoryError
   *   Indicates that there is insufficient memory for the new list.    
   **/   
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(1) startnode and endnode are the same.
   //
   public static ObjectNode[ ] listPart(ObjectNode start, ObjectNode end)
   {
      ObjectNode copyHead;
      ObjectNode copyTail;
      ObjectNode cursor;
      ObjectNode[ ] answer = new ObjectNode[2];
      
      // Make the first node for the newly created list. Notice that this will
      // cause a NullPointerException if start is null.
      copyHead = new ObjectNode(start.data, null);
      copyTail = copyHead;
      cursor = start;
      
      // Make the rest of the nodes for the newly created list.
      while (cursor != end)
      {
         cursor = cursor.link;
         if (cursor == null)
            throw new IllegalArgumentException
            ("end node was not found on the list");
         copyTail.addNodeAfter(cursor.data);
         copyTail = copyTail.link;
      }
      
      // Return the head and tail references
      answer[0] = copyHead;
      answer[1] = copyTail;
      return answer;
   }        
   
   
   /**
   * Find a node at a specified position in a linked list.
   * @param head
   *   the head reference for a linked list (which may be an empty list in
   *   which case the head is null)
   * @param position
   *   a node number
   * @precondition
   *   position &gt; 0.
   * @return
   *   The return value is a reference to the node at the specified position in
   *   the list. (The head node is position 1, the next node is position 2, and
   *   so on.) If there is no such position (because the list is too short),
   *   then the null reference is returned.
   * @exception IllegalArgumentException
   *   Indicates that position is not positive.    
   **/
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(1) the position we looking for is the first one.
   //
   public static ObjectNode listPosition(ObjectNode head, int position)
   {
      ObjectNode cursor;
      int i;
      if (head==null)
    	  return null;
      if (position < 0)
           throw new IllegalArgumentException("position is not positive");
      
      cursor = head;
      for (i = 0; (i < position) && (cursor != null); i++)
         cursor = cursor.link;

      return cursor;
   }


   /**
   * Search for a particular piece of data in a linked list.
   * @param head
   *   the head reference for a linked list (which may be an empty list in
   *   which case the head is null)
   * @param target
   *   a piece of data to search for
   * @return
   *   The return value is a reference to the first node that contains the
   *   specified target. If there is no such node, the null reference is 
   *   returned.     
   **/   
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(1) the node we looking for is the first element.
   //
   public static ObjectNode listSearch(ObjectNode head, Object target)
   {
      ObjectNode cursor;
      
      for (cursor = head; cursor != null; cursor = cursor.link)
         if (target == cursor.data)
            return cursor;
        
      return null;
   }

   
   /**
   * Modification method to remove the node after this node.   
   * @precondition
   *   This node must not be the tail node of the list.
   * @postcondition
   *   The node after this node has been removed from the linked list.
   *   If there were further nodes after that one, they are still
   *   present on the list.
   * @exception NullPointerException
   *   Indicates that this was the tail node of the list, so there is nothing
   *   after it to remove.
   **/
   //presume we get N node in total in the linked list.
   //O(N)
   //Ω(N)
   //θ(N)
   public void removeNodeAfter( )   
   {
      link = link.link;
   }          
   
   
   /**
   * Modification method to set the data in this node.   
   * @param newData
   *   the new data to place in this node
   * @postcondition
   *   The data of this node has been set to newData.
   **/
   public void setData(Object newData)   
   {
      data = newData;
   }                                                               
   
   
   /**
   * Modification method to set the link to the next node after this node.
   * @param newLink
   *   a reference to the node that should appear after this node in the linked
   *   list (or the null reference if there is no node after this node)
   * @postcondition
   *   The link to the node after this node has been set to newLink.
   *   Any other node (that used to be in this link) is no longer connected to
   *   this node.
   **/
   public void setLink(ObjectNode newLink)
   {                    
      link = newLink;
   }
   
   
   @Override
   public String toString() 
   {
	   String result;
	   ObjectNode tail;
	   if (data==null)
		   return "no result ";
	   result=""+data;
	   tail=link;
	   while(tail!=null) {
		   result+=tail.data;
		   tail=tail.link;
	   }
	   
	   return result;
   }
   
   public static void main(String[] args) {
	   ObjectNode newHead;
	   String s=new String("ABCDEFGHIJKLMNOPQRSTUVWXYZ");
	   int index=0;
	   int size_newHead;
	   
	   newHead=new ObjectNode(s.charAt(index), null);
	   for (index=25;index>0;index--) {
		   newHead.addNodeAfter(s.charAt(index));
	   }
	   System.out.println(newHead);
	   
	   
	   size_newHead=listLength(newHead);
	   System.out.print("Number of nodes = ");
	   System.out.println(size_newHead);
	   int size_rec_newHead;
	   size_rec_newHead=listLength_rec(newHead);
	   System.out.print("Number of nodes = ");
	   System.out.println(size_rec_newHead);
	   
	   ObjectNode k=listCopy(newHead);
	   System.out.println(k);
	   
	   int size_k;
	   size_k=listLength(k);
	   System.out.print("Number of nodes = ");
	   System.out.println(size_k);
	   int size_rec_k;
	   size_rec_k=listLength_rec(k);
	   System.out.print("Number of nodes = ");
	   System.out.println(size_rec_k);
	   
	   ObjectNode k2=listCopy(newHead);
	   System.out.println(k2);
	   
	   int size_k2;
	   size_k2=listLength(k2);
	   System.out.print("Number of nodes = ");
	   System.out.println(size_k2);
	   int size_rec_k2;
	   size_rec_k2=listLength_rec(k2);
	   System.out.print("Number of nodes = ");
	   System.out.println(size_rec_k2);
	   
   }
}
           
```

Second, code for singlyLinkedlist
```
package edu.colorado.nodes;
public class SinglyLinkedList {
/**
 * 
 * @param args
 * 
 * This class provides iterator methods:
 * reset: to reset the iteration - starting from the head of the list.
 * next: returns the element pointed to by the iterator and increments the iterator to the next node.
 * hasNext: returns true if the iterator points to an existing node and false otherwise.
 * 
 */
	
	private ObjectNode head;
	private ObjectNode tail;
	private ObjectNode iterator;
	int countNodes;
	
	// Add a new node at the very end of the list
	//O(1)
	public void addAtEndNode(Object c) {
		if (tail==null) {
			ObjectNode node=new ObjectNode(c, null);
			head=node;
			tail=head;
			iterator=head;
			countNodes+=1;
		}else {
			ObjectNode node=new ObjectNode(c, null);
			tail.setLink(node);
			tail=node;
			countNodes+=1;
		}
	}
	//Add a new node at the very begining of the list
	public void addAtFrontNode(Object c) {
		if (head==null) {
			ObjectNode node=new ObjectNode(c, null);
			head=node;
			tail=head;
			iterator=head;
			countNodes+=1;
		}else {
			ObjectNode node=new ObjectNode(c, null);
			node.setLink(head);
			head=node;
			countNodes+=1;
		}
	}
	
	// reset the iterator to the beginning of the list.
	public void reset() {
		iterator=head;
	}
	
	// move the iterator to the next node.
	public Object next() {
		Object iteratorObject=iterator.getData();
		iterator=iterator.getLink();
		return iteratorObject;
	}
	
	//return a boolean to show if iterator get to the end of the list
	public boolean hasNext() {
		return iterator!=null;
	}
	
	//return the int number of the nodes
	public int countNodes() {
		return countNodes;
	}
	
	// return the exact object on the list at the index
	public Object getObjectAt(int i) {
		ObjectNode cursor=head;
		if (i<0 || i>countNodes-1) {
			throw new IllegalArgumentException
            ("index exceeds range");
		}else {
			for (int index=0;index<i;index++) {
				cursor=cursor.getLink();
			}
		}
		return cursor.getData();
	}
	
	//return the object of the last node.
	public Object getLast() {
		return tail.getData();
	}
	
	// print all object in the node on the list
	public String toString() {
		String result;
		ObjectNode curTail;
		Object data=head.getData();
		if (data==null)
			   return "no result ";
		result=""+data;
		curTail=head.getLink();
		while(curTail!=null) {
			result+=curTail.getData();
			curTail=curTail.getLink();
		   }
		return result;
	}

	public static void main(String[] args) {
		SinglyLinkedList newList;
		newList=new SinglyLinkedList();
		
		//SinglyLinkedList newList;
		newList=new SinglyLinkedList();
		newList.addAtFrontNode("c");
		newList.addAtFrontNode("b");
		newList.addAtFrontNode("a");
		newList.addAtEndNode("a");
		newList.addAtEndNode("b");
		System.out.println(newList);
		
		newList.reset(); 
		while(newList.hasNext()) {
			System.out.println(newList.next()); 
			}
	}
}
```



### PartII
In this part, we are going to program based on the SinglyLinkedList and BigInteger. By BigInteger, it is a class used for mathematical operation which involves very big integer calculations that are outside the limit of all available primitive data types.

```
package edu.colorado.nodes;

import java.math.BigInteger;
import java.util.Scanner;

public class MerkleHellman {
	private static SinglyLinkedList w;
	private static SinglyLinkedList b;
	private static BigInteger q;
	private static BigInteger r;

	//the code about binaryString is copied from 
	//https://stackoverflow.com/questions/917163/convert-a-string-like-testing123-to-binary-in-java
	public static String binaryString(String s) {
	  byte[] bytes = s.getBytes();
	  StringBuilder binary = new StringBuilder();
	  for (byte b : bytes)
	  {
	     int val = b;
	     for (int i = 0; i < 8; i++)
	     {
	        binary.append((val & 128) == 0 ? 0 : 1);
	        val <<= 1;
	     }
	  }
	  System.out.println("'" + s + "' to binary: " + binary);
	  return binary.toString();
	}
	
	// pass in a string provided by users and return the decimal number calculated by keys and binary list of the string, 
	// which is kept in Biginteger.
	public static BigInteger encryption(String str) {
		String binaryStr=binaryString(str);
		BigInteger sum=new BigInteger("0");
		for (int i=0;i<binaryStr.length();i++) {
			BigInteger num=BigInteger.valueOf(Character.getNumericValue(binaryStr.charAt(i)));
			
			BigInteger bValue=(BigInteger)b.next();
			sum=sum.add(num.multiply((bValue)));
		}
		
		
		return sum;
		
	}
	
	// using encryption result and algorithm mentioned on the pdf, we can decrypte the string
	public static String decryption(BigInteger encryp,String str) {
		BigInteger result;
		int strBits=str.length()*8;
		result= r.modInverse(q);
		result=(encryp.multiply(result)).mod(q);
		String decryBits="";
		for (int i=w.countNodes-1;i>=0;i--) {
			BigInteger tem=(BigInteger)w.getObjectAt(i);
			//System.out.println(tem);
			if (result.compareTo(tem)==-1) {
				decryBits="0"+decryBits;
			}else {
				decryBits="1"+decryBits;
				result=result.subtract(tem);
			}
		
		}
		decryBits=decryBits.substring(0,strBits);
		//System.out.println(decryBits);
		
		
		//convert binary code to texts.
		String bits8;
		String stringText="";
		for (int index = 0;index < decryBits.length(); index = index + 8) {
			bits8=decryBits.substring(index,index+8);
			
			stringText+= new Character((char) Integer.parseInt(bits8, 2)).toString();//this code below copy from https://github.com/RachelOuyang/Merkle-Hellman-
			// /blob/master/src/merklehellman/Crypto.java
		}
		
		System.out.println("decryption: "+stringText);
		return stringText;
	}

	
	public static void main(String[] args) {
		//generate super-increasing list w.
		w=new SinglyLinkedList();
		BigInteger nodeNum=new BigInteger("1");
		BigInteger sum=new BigInteger("1");
		w.addAtEndNode(nodeNum);
		int count=1;
		
		while(count<640) {
			BigInteger nextNum;
			BigInteger c= new BigInteger("1");
			
			nextNum=sum.add(c);
			
			
			sum=sum.add(nextNum);
			w.addAtEndNode(nextNum);
			count++;
		}
		//generate the q which is a number that is greater than sum. Choose ten more.
		q=sum.add(BigInteger.TEN);
		//generate the r which is in range of [1,q) and is coprime to q.
		r=q.subtract(BigInteger.ONE);
		BigInteger gcd=q.gcd(r);
		while (gcd.compareTo(BigInteger.ONE)!=0 && r.compareTo(BigInteger.ONE)>0) {
			r=r.subtract(BigInteger.ONE);
		}
		
		//generate public key b.
		b=new SinglyLinkedList();
		BigInteger bNum;
		
		while (w.hasNext()) {
			bNum=(BigInteger)w.next();
			bNum=(bNum.multiply(r)).mod(q);
			b.addAtEndNode(bNum);
		}
		w.reset();
		
		Scanner in= new Scanner(System.in);
		String str = in.nextLine();
		//Stop program if str is longer than 80 characters. 
		if (str.length()>80) {
			System.out.println("Please enter string that is shorter than 80 letters");
			return;
		}
			
		
		//Encryption
		BigInteger encryptionResult=encryption(str);
		System.out.println("encryption:"+encryptionResult);
		
		//Decryption 
		String decrytionResult=decryption(encryptionResult,str);
		
	}
}

```
### PartIII
Last, code for MerkleTree. 
Note: FOR TEST FILE, I used relative path. Therefore, if you want to test the code, you need to change the path according to the file location in you computer. 

```
package edu.colorado.nodes;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class MerkleTree {
	private static SinglyLinkedList list;
	private static SinglyLinkedList line1;
	private static SinglyLinkedList line2;
	
	public static void readFileByLines(String fileName) {
        File file = new File(fileName);
        BufferedReader reader = null;
        try {
     
            reader = new BufferedReader(new FileReader(file));
            String tempString = null;
            int node = 0;
            // read each line.
            while ((tempString = reader.readLine()) != null) {
                // store the data.
                //System.out.println("line " + node + ": " + tempString);
                line1.addAtEndNode(tempString);
                node++;
            }
            if (node%2!=0) {
            	String tem=(String)line1.getLast();
            	line1.addAtEndNode(tem);
            }
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e1) {
                }
            }
        }
    }
	
	public static String h(String text)  {
		try {
			MessageDigest digest = MessageDigest.getInstance("SHA-256");
			byte[] hash =digest.digest(text.getBytes(StandardCharsets.UTF_8));
			StringBuffer sb = new StringBuffer();
			for (int i = 0; i <= 31; i++) {
				byte b = hash[i];
				sb.append(String.format("%02X", b));
			}
			return sb.toString();
		    }
		    catch (NoSuchAlgorithmException e) {
		    	
		        System.err.println("I'm sorry, but MD5 is not a valid message digest algorithm");
		        return "error";
		    }
	}

	public static void buildLine1() {
		line1=new SinglyLinkedList();
		//should change the path below, where I directly use a relative path.
		readFileByLines("/Users/yuanpenc/Desktop/a4.txt");
		//System.out.println(line1.countNodes);
		//System.out.println((String)line1.getLast());
		list.addAtEndNode(line1);
		
	}

	
	public static void buildLine2() {
		line2=new SinglyLinkedList();
		line1.reset(); 
		while(line1.hasNext()) {
			line2.addAtEndNode(h((String)line1.next()));
			}
		list.addAtEndNode(line2);
		nextLine();
		
	}
	
	public static void nextLine() {
		SinglyLinkedList nLine=new SinglyLinkedList();
		SinglyLinkedList lastLine=(SinglyLinkedList)list.getLast();
	
		lastLine.reset(); 
		int count=1;
		String result="";
		while(lastLine.hasNext()) {
			result=result+(String)lastLine.next();
			
			if (count%2==0) {//even
				//System.out.println(h(result));
				nLine.addAtEndNode(h(result));
				result="";
			}
			//line2.addAtEndNode(h((String)line1.next()));
			count++;
		}
		list.addAtEndNode(nLine);
	}
	
	
	public static void main(String[] args) {
		list=new SinglyLinkedList();
		buildLine1();
		buildLine2();
		while(((SinglyLinkedList)list.getLast()).countNodes!=1) {
			SinglyLinkedList lastLine;
			lastLine=(SinglyLinkedList)list.getLast();
			if (lastLine.countNodes%2!=0){//odd nodes
				lastLine.addAtEndNode(lastLine.getLast());
				
			}
			nextLine();
			System.out.println("count="+lastLine.countNodes);
		}
		
		System.out.println(list.getLast());
	}

}

```

# Queues&RedBlackTrees
Write a spell checker that is based on a red black tree. The execution of the program, when run with shortWords.txt as a command line argument, will appear as follows:

java RedBlackTreeSpellChecker shortwords.txt
Loading a tree of English words from shortwords.txt.
Red Black Tree is loaded with 10 words.
Initial tree height is 3.
Never worse than 2 * Lg( n+1) = 6.918804721654216.

Legal commands are: 
d   display the entire word tree with a level order traversal.
s    print the words of the tree in sorted order (using an inorder traversal).
r    print the words of the tree in reverse sorted order (reverse inorder traversal). 
c   <word> to spell check this word.
a   <word> add this word to tree.
f   <fileName> to check this text file for spelling errors.
i   display the diameter of the tree.
m  view this menu.
!   to quit.
Result example

```
c  aaa
aaa Not in dictionary. Perhaps you mean
aa
>c aa
Found aa after 3 comparisons
>a mike
mike was added to dictionary.
>c mike
Found mike after 4 comparisons
>c mik
mik Not in dictionary. Perhaps you mean
mike
>a mik
mik was added to dictionary.
>d
Level order traversal
[data = aal:Color = Black:Parent = -1: LC = a: RC = aam]
[data = a:Color = Black:Parent = aal: LC = Aani: RC = aa]
[data = aam:Color = Black:Parent = aal: LC = aalii: RC = aardwolf]
[data = Aani:Color = Black:Parent = a: LC = A: RC = Aaron]
[data = aa:Color = Black:Parent = a: LC = -1: RC = -1]
[data = aalii:Color = Black:Parent = aam: LC = -1: RC = -1]
[data = aardwolf:Color = Red:Parent = aam: LC = aardvark: RC = mike]
[data = A:Color = Red:Parent = Aani: LC = -1: RC = -1]
[data = Aaron:Color = Red:Parent = Aani: LC = -1: RC = -1]
[data = aardvark:Color = Black:Parent = aardwolf: LC = -1: RC = -1]
[data = mike:Color = Black:Parent = aardwolf: LC = mik: RC = -1]
[data = mik:Color = Red:Parent = mike: LC = -1: RC = -1]
>c aalii
Found aalii after 3 comparisons
>!
Bye.
```

Code for this part:
* Queen
```
import java.util.ArrayList;
import java.util.List;

public class Queue {

	private int front;
	private int rear;
	private int size=10;
	private Object[] data;

	public Queue() {
		front=0;
		rear=0;
		data=new Object[size];
	}
	
	
	// Pre-condition: queue not empty.
	public Object deQueue() {
		if (rear==0) {
			return null;
		}
		Object[] newDataList=new Object[size];
		Object frontData=data[front];
		System.arraycopy(data, 1, newDataList, 0, size-1);
		rear=rear-1;
		data=newDataList;
		return frontData;
	}
	
	public void doubleList() {
		int tempSize=size;
		size=size*2;
		Object[] newDataList=new Object[size];
		System.arraycopy(data, 0, newDataList, 0, tempSize);
		data=newDataList;
		
	}
	
    //Pre-condition Memory is available for doubling queue capacity when full. 
	//Post-condition: queue now contains newData in the rear.
	public void enQueue(Object newData) {
		if (rear==size) {
			doubleList();
		}
		data[rear]=newData;
		rear=rear+1;
	}
	
	
	//Pre-condition: queue not empty.
	public Object getFront() {
		return data[front];
		
	}
	
	public boolean isEmpty() {
		return rear==0;
		
	}
	
	public boolean isFull() {
		return rear==size-1;
	}
	
	public String toString() {
		List<Object> list1=new ArrayList<>();
		for (int i=0;i<size;i++) {
			list1.add( data[i]);
		}
		String strResult=list1.toString();
		return strResult;
		
	}
	
	public static void main(String[] args) {
		/**
		Queue newQueue;
		newQueue=new Queue();
		for (int i=0;i<20;i++) {
			newQueue.enQueue(i);
		}
		//System.out.print(newQueue.size);
		
		//newQueue.enQueue(10);
		newQueue.deQueue();
		System.out.print(newQueue);
		*/
	}
}
```
* RedBlackNode

```

public class RedBlackNode {
	private RedBlackNode p;
	private RedBlackNode lc;
	private RedBlackNode rc;
	private int color;
	private String data;
	
	public RedBlackNode(String data, int color, RedBlackNode p, RedBlackNode lc, RedBlackNode rc){
		this.data=data;
		this.color=color;
		this.p=p;
		this.lc=lc;
		this.rc=rc;
	}
	
	public int getColor() {
		return color;
	}
	
	public String getData() {
		return data;
	}
	
	public RedBlackNode getLc() {
		return lc;
	}
	
	public RedBlackNode getP() {
		return p;
	}
	
	public RedBlackNode getRc() {
		return rc;
	}
	
	public void setColor(int color) {
		this.color=color;
	}
	
	public void setData(String data) {
		this.data=data;
	}
	
	public void setLc(RedBlackNode lc) {
		this.lc=lc;
	}
	
	public void setRc(RedBlackNode rc) {
		this.rc=rc;
	}
	
	public void setP(RedBlackNode p) {
		this.p=p;
	}
	
	public String toString() {
		return data;
	}
}

```

* RedBlackTree

```
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class RedBlackTree {
	private RedBlackNode root;
	private RedBlackNode sentinel;
	private int size;
	private List<String> listS=new ArrayList<>();
	private int compareCount;
	
	public RedBlackTree() {
		root=null;
		sentinel=new RedBlackNode("-1",0,null,null,null);
		
	}
	
	
	public RedBlackNode getRoot() {
		return root;
	}
	
	
	//O(n)
	//Ω(n)
	//Θ(n)
	public void readFileByLines(String fileName,RedBlackTree t) {
		File file = new File(fileName);
        BufferedReader reader = null;
        try {
     
            reader = new BufferedReader(new FileReader(file));
            String tempString = null;
            int node = 0;
            // read each line.
            while ((tempString = reader.readLine()) != null) {
                // store the data.
                //System.out.println("line " + node + ": " + tempString);
            	//t.listS.add(tempString);
                t.insert(tempString);
                node++;
            }
            t.size=node;
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e1) {
                }
            }
        }
	}
	
	//Pre-condition:memory is available for insertion.
	//O(Log n)
	//Ω(Log n)
	//Θ(Log n)
	public void insert(String value) {
		listS.add(value);
		RedBlackNode y=sentinel;
		RedBlackNode x=root;
		if (root!=null) {
			while (x!=sentinel) {
				y=x;
				//System.out.println(value);
				//System.out.println(1);
				
				if ((value.compareTo(x.getData()))<0) {
					x=x.getLc();
				}else {
					x=x.getRc();
				}
			}
		}
		RedBlackNode newRbn=new RedBlackNode(value,1,null,null,null);
		newRbn.setP(y);
		if(y==sentinel) {
			root=newRbn;
		}else {
			if ((value.compareTo(y.getData()))<0) {
				y.setLc(newRbn);
			}else {
				y.setRc(newRbn);
			}
		}
		newRbn.setLc(sentinel);
		newRbn.setRc(sentinel);
		newRbn.setColor(1);
		//System.out.println("father:"+newRbn);
		//System.out.println("fathercolor:"+newRbn.getP().getColor());
		RBInsertFixup(newRbn);
	}
	
	//pre: right[x] != nil[T].
	//root's parent is nill[T].
	//O(1)
	//Ω(1)
	//Θ(1)
	public void leftRotate(RedBlackNode x) {
		RedBlackNode y=x.getRc();
		x.setRc(y.getLc());
		y.getLc().setP(x);
		y.setP(x.getP());
		
		if(x.getP()==sentinel) {
			root=y;
		}else {
			if(x==x.getP().getLc()) {
				x.getP().setLc(y);
			}else {
				x.getP().setRc(y);
			}
		}
		y.setLc(x);
		x.setP(y);
	}
	
	//pre: left[x] != nil[T]
	//pre: root's parent is nill[T]
	//O(1)
	//Ω(1)
	//Θ(1)
	public void rightRotate(RedBlackNode x) {
		RedBlackNode y=x.getLc();
		x.setLc(y.getRc());
		y.getRc().setP(x);
		y.setP(x.getP());
		
		if (x.getP()==sentinel) {
			root=y;
		}else {
			if (x==x.getP().getLc()) {
				x.getP().setLc(y);
			}else {
				x.getP().setRc(y);
			}
		}
		y.setRc(x);
		x.setP(y);
	}
	
	//O(1)
	//Ω(1)
	//Θ(1)
	public void RBInsertFixup(RedBlackNode z) {
		while (z.getP().getColor()==1) {
			//System.out.println(z.getP().getP());
			if (z.getP()==z.getP().getP().getLc()) {
				//System.out.println("hi");
				RedBlackNode uncle=z.getP().getP().getRc();
				if (uncle.getColor()==1) {
					//uncle is red
					z.getP().setColor(0);
					uncle.setColor(0);
					z.getP().getP().setColor(1);
					z=z.getP().getP();
				}else {
					if (z==z.getP().getRc()) {
						z=z.getP();
						leftRotate(z);
					}
					z.getP().setColor(0);
					z.getP().getP().setColor(1);
					rightRotate(z.getP().getP());
				}
			}else {//rigit side
				RedBlackNode uncle=z.getP().getP().getLc();
				if (uncle.getColor()==1) {
					z.getP().setColor(0);
					uncle.setColor(0);
					z.getP().getP().setColor(1);
					z.getP().getP();
				}else {
					if(z==z.getP().getLc()) {
						z=z.getP();
						rightRotate(z);
					}
					z.getP().setColor(0);
					z.getP().getP().setColor(1);
					leftRotate(z.getP().getP());
				}//end else
			}//end else
		}//end while
		root.setColor(0);
	}
	
	public void printData(RedBlackNode node) {
		String result;
		result="data = "+node.getData()+":Color = "+node.getColor()+":Parent = "+node.getP()+":LC = "+node.getLc()+":RC = "+node.getRc();
		System.out.println(result);
	}
	

	public void inOrderTraversal() {
		inOrderTraversal(root);
	}
	
	//O(n)
	//Ω(n)
	//Θ(n)
	public void inOrderTraversal(RedBlackNode a) {
		if (a==null) {
			return;
		}
		inOrderTraversal(a.getLc());
		printData(a);
		inOrderTraversal(a.getRc());
		
		
	}
	
	public int height() {
		return height(root);
	}
	
	//O(log n)
	//Ω(log n)
	//Θ(log n)
	public int height(RedBlackNode t) {
		if (t==null) {
			return -1;
		}
		if (t.getData()==null) {
			return -1;
		}
		else {
			int lHeight=height(t.getLc());
			int rHeight=height(t.getRc());
	
			if (lHeight>rHeight) {
				return (lHeight+1);
			}else {
				return (rHeight+1);
			}
		}
		
	}
	
	
	//O(n)
	//Ω(n)
	//Θ(n)
	public void levelOrderTraversal() {
		if(root==null) {
			return;
		}
		Queue q=new Queue();
		q.enQueue(root);
		RedBlackNode node;
		while(!q.isEmpty()) {
			node=(RedBlackNode) q.deQueue();
			printData(node);
			if (node.getLc()!=sentinel) {
				q.enQueue(node.getLc());
			}
			if (node.getRc()!=sentinel) {
				q.enQueue(node.getRc());
			}
		}
	}
	
	public void reverseOrderTraversal() {
		reverseOrderTraversal(root);
	}
	
	
	//O(n)
	//Ω(n)
	//Θ(n)
	public void reverseOrderTraversal(RedBlackNode t) {
		if (t==null) {
			return;
		}
		reverseOrderTraversal(t.getRc());
		printData(t);
		reverseOrderTraversal(t.getLc());
	}
	
	public int getSize() {
		return size;
	}
	
	
	//O(n)
	//Ω(n)
	//Θ(n)
	public String closeBy(String v) {
		int leastLength=0;
		int mostLength=10000;
		String mostString="";
		String leastString="";
		for (int j=0;j<listS.size();j++) {
			String newString=listS.get(j);
			if (v.startsWith(newString)) {
				if (newString.length()>leastLength) {
					leastString=newString;
				}
			}
			if (newString.startsWith(v)) {
				if (newString.length()<mostLength) {
					mostString=newString;
				}
			}
		}
		if (Math.abs(v.length()-leastLength)<=Math.abs(v.length()-mostLength)) {
			if(leastString.length()!=0) {
				//System.out.println("leastString:"+leastString);
				return leastString;
			}
		}
		//System.out.println("mostString:"+mostString);
		if (mostString.length()!=0) {
			return mostString;
		}
		return "No matching String";
	}
	
	//O(n)
	//Ω(n)
	//Θ(n)
	public boolean contains(String v) {
		int j;
		for (j=0;j<listS.size();j++) {
			String newString=listS.get(j);
			if (v.compareTo(newString)==0) {
				compareCount=j+1;
				return true;
			}
		}
		compareCount=j;
		return false;
	}
	
	public int getRecentCompares() {
		return compareCount;
	}
	
	
	public static void main(String[] args) {
		RedBlackTree rbt =new RedBlackTree();
		//rbt.readFileByLines("/Users/yuanpenc/Desktop/shortwords.txt",rbt);
		// after 1..5 are inserted
		for(int j = 1; j <= 5; j++) rbt.insert(""+j);
        System.out.println("RBT in order");
        rbt.inOrderTraversal();
        System.out.println("RBT level order");
        rbt.levelOrderTraversal();
        //rbt.insert("abc");
        //rbt.insert("a");
        
       // is 3 in the tree
        
        if(rbt.contains(""+3)) System.out.println("Found 3");
        else System.out.println("No 3 found"); 
        
        // display the height
        System.out.println("The height is " + rbt.height());  
        
        //System.out.println(rbt.closeBy("ab"));
        //System.out.println(rbt.root.getLc().getLc().getData());
		
		//rbt.insert("D");
		//rbt.insert("B");
		//rbt.insert("C");
		//rbt.insert("H");
		//rbt.insert("J");
		//System.out.println(rbt.root.getRc());
	}
}
```

* RedBlackTreeTester
```
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class RedBlackTreeTester {
	
	private static int diameter=0;
	
	//read the content in a new file for command f.
	public static List<String> readFileByLines(String fileName) {
		File file = new File(fileName);
        BufferedReader reader = null;
        List<String> ls=new ArrayList<>();
        try {
     
            reader = new BufferedReader(new FileReader(file));
            String tempString = null;
     
            // read each line.
            while ((tempString = reader.readLine()) != null) {
                // store the data.
                //System.out.println("line " + node + ": " + tempString);
            	//t.listS.add(tempString);
                ls.add(tempString);
                
            }
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e1) {
                }
            }
        }
        return ls;
	}
	
	public static int diameterOfBinaryTree(RedBlackNode root) {
        diameter=0;
        diameterHelper(root);
        return diameter;
	}
	
	public static int diameterHelper(RedBlackNode root) {
		if (root == null) return 0;
		int l = diameterHelper(root.getLc());
        int r = diameterHelper(root.getRc());
        if (l + r > diameter) diameter = l + r;
        return Math.max(l, r) + 1;
	}
	
	//pre-condition: the path need to change if user want to test different file or on different computer. 
	public static void main(String[] args) {
		RedBlackTree rbt =new RedBlackTree();
		String path="/Users/yuanpenc/Desktop/shortwords.txt";
		rbt.readFileByLines(path,rbt);
		//System.out.println(command);
		boolean quit=false;
		while(true) {
			Scanner input=new Scanner(System.in);
			String command=input.nextLine();
			switch(command) {
			case "d":
				System.out.println("RBT level order");
		        rbt.levelOrderTraversal();
				break;
			case "s":
				System.out.println("RBT in order");
		        rbt.inOrderTraversal();
				break;
			case "r":
				System.out.println("RBT in reserve order");
		        rbt.reverseOrderTraversal();
		        break;
		        
			case "c":
				System.out.println("spell check this word");
				Scanner wordInput=new Scanner(System.in);
				String word=wordInput.nextLine();
				if(rbt.contains(word)) {
					int count=rbt.getRecentCompares();
					System.out.println("found "+word+" after "+count+" comparisons ");
				}else {
					
					System.out.println(word+" Not in dictionary. Perhaps you mean "+rbt.closeBy(word));
				}
		        break;    
			case "a":
				
				Scanner wordInsert=new Scanner(System.in);
				String wordIn=wordInsert.nextLine();
				System.out.println(" was added to dictionary.");
		        rbt.insert(wordIn);
		        break;
		    
			case "f":
				System.out.println("enter a path");
				Scanner filePath=new Scanner(System.in);
				String newFilePath=filePath.nextLine();
				List<String> ls=readFileByLines(newFilePath);
				for (int i=0;i<ls.size();i++) {
					String findWord=ls.get(i);
					if(rbt.contains(findWord)) {
						int count=rbt.getRecentCompares();
						System.out.println("found "+findWord+" after "+count+" comparisons ");
					}else {
						
						System.out.println(findWord+" Not in dictionary. Perhaps you mean "+rbt.closeBy(findWord));
					}
				}
				break;
		        
			case "i":
				diameterOfBinaryTree(rbt.getRoot());
				System.out.println("the diameter of the tree is "+diameter);
				break;
		        
			case "!":
				quit=true;
			
			}
			if (quit) {
				break;
			}
		}
	}
}
```
