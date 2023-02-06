# **Lab Report 2 - Servers & Bugs (Week 3)**

# **Part 1**
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String word = "empty";
    ArrayList<String> wordList = new ArrayList<>();

    /**
     * Method that prints out the list of strings
     * 
     * @param list string array list
     * @return prints out the strings
     */
    public static String printStrings(ArrayList<String> list) {
        StringBuilder result = new StringBuilder();
        for (int i = 0; i < list.size(); i++) {
            result.append(list.get(i));
            if (i < list.size()-1) {
                result.append("\n");
            }
        }
        return result.toString();
    }

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(word);
        }
        else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    word = parameters[1];
                    wordList.add(word);
                }
            }
            return printStrings(wordList);
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
![Image](https://github.com/jcaylao/LabReport2/blob/main/Screenshot%202023-02-05%20140628.png?raw=true)

First *handleRequest* is called, the relevant arguments of handleRequest is a url of type URI. *Parameters* is a string array that contains strings of the url. The value of the variable *word* gets assigned to empty at first and then once I input the add request *word* is reassigned to the string *"Hi"*. *wordList* starts off as an empty arraylist, after I inputted the add request it contains 1 element which is the string *"Hi"*.

Then *printStrings* method is called, the relevant arguments of printStrings is an arraylist of type String. The stringBuilder *result* starts off as empty then elements of list are appended.

![Image](https://user-images.githubusercontent.com/122569462/216848724-2effe37c-ae58-46a6-ad49-aa7fb1ecab5d.png)

First *handleRequest* is called, the relevant arguments of handleRequest is a url of type URI. *Parameters* is a string array that contains strings of the url. The value of the variable *word* is *"Hi"* and then once I input the add request *word* is reassigned to the string *"my name is jaira"*. *wordList* contains only 1 element which is the string *"Hi"*, then *"my name is jaira"* is added which results in wordList containing 2 elements.

Then *printStrings* method is called, the relevant arguments of printStrings is an arraylist of type String. The stringBuilder *result* starts off as empty then elements of list are appended.

# **Part 2**

**A failure-inducing input for the buggy program**
```
  @Test
  public void testReverseInPlaceFail() {
    int[] input2 = {8,9,10};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[]{10,9,8}, input2);
  }
 ```
 
 **An input that doesn’t induce a failure**
 ```
 	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 555 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 555 }, input1);
	}
```

**The symptom, as the output of running the tests**
![Image](https://github.com/jcaylao/LabReport2/blob/main/Screenshot%202023-02-06%20124844.png?raw=true)

**The bug, as the before-and-after code change required to fix it**
**Before:** ![Image](https://github.com/jcaylao/LabReport2/blob/main/Screenshot%202023-02-06%20125040.png?raw=true)
**After:** ![Image](https://github.com/jcaylao/LabReport2/blob/main/Screenshot%202023-02-06%20125142.png?raw=true)

# **Part 3**

In lab of week 2, I learned how to download code from my repository and uploade changes using Github Desktop. This class is my first time getting introduced to github and so this was also my first time getting introduced to Github desktop. Although this was my first time, the lab write-up made this process easy because it was really easy to follow along through the steps given. This process also included learning how to commit and push the changes I made in order for it to appear on Github. Learning this was really useful because I have used this method of downloading code and cloning repositories through Github Desktop multiple times in some of the future labs. 
