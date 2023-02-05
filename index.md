# **Lab Report 2 - Servers & Bugs (Week 3)**

# **Part 1**
`import java.io.IOException;
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
}`
hello
