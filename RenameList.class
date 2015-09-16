/*
 * Program to rename huge list of files following a single plain file instructions
 * It will look for an instructions file with the following format:
 * OLD SYSTEM [#].ext|[#]NewSystem.ext
 * @author Danilo Josué Ramírez Mattey
 * @year 2015
*/
import java.lang.String;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.regex.*;

class RenameLists { 
  
  private String rulefile = "rename.sc";
  private String rule;
  private int normalPause = 600;
  private int processPause = 75;
  
  public static void main(String[] args){
    RenameLists rl = new RenameLists();
    rl.main_process();
    return;
  } 
  
  
  public void main_process(){
    this.presentation();
    this.pauseProgram(this.normalPause);
    if(this.searchFile() == false){
      this.terminateProgram("Rules file "+this.rulefile+" does not exist, its empty or cannot be readed.");
      return;
    }
    this.pauseProgram(this.normalPause);
    this.listAllFiles();
    this.pauseProgram(this.normalPause);
    this.terminateProgram("Program finished");
  }
  
  private void listAllFiles(){
    this.processMessage("Ready to execute process.");
    this.pressAnyKeyToContinue();
    String[] ruleAndTarget = this.rule.split(Pattern.quote("|"));
    //String pattern = "DBZ(.*)?";
    String pattern = ruleAndTarget[0];
    pattern = pattern.replace("[#]","(\\d+)");
    pattern = pattern.replace("[","\\[");
    pattern = pattern.replace("]","\\]");
    pattern = pattern.replace(".","\\.");
    Pattern r = Pattern.compile(pattern);
    this.processMessage("");
    this.processMessage("Listing all files that match the pattern "+pattern+":");
    File folder = new File(".");
    File[] listOfFiles = folder.listFiles();
    
    for (int i = 0; i < listOfFiles.length; i++) {
      if (listOfFiles[i].isFile()) {
        Matcher m = r.matcher(listOfFiles[i].getName());
        if (m.find( )) {
          //System.out.println("Found value: " + m.group(0) );
          String newName = ruleAndTarget[1];
          newName = newName.replace("[#]",m.group(1));
          this.processMessage("=> File " + listOfFiles[i].getName()+ " --- " +m.group(0)+" --- "+m.group(1)+" --- "+newName);
          listOfFiles[i].renameTo(new File(newName));
          //System.out.println("Found value: " + m.group(1) );
          //System.out.println("Found value: " + m.group(2) );
          this.pauseProgram(this.processPause);
        }
        
      }
    }
     this.processMessage("");
  }
  
  private void presentation(){
    System.out.println("********************************************");
    System.out.println("*                 WELCOME                  *");
    System.out.println("********************************************");
    System.out.println("@ The following application will rename all files in");
    System.out.println("@ as folder following a group of rules being indicated in a "+this.rulefile+" file");
    System.out.println("@ located in the same folder");
    System.out.println(" ");
    
  }
  private boolean searchFile(){
    this.processMessage("Searching for rules file");
    File f = new File(this.rulefile);
    if(f.exists() && !f.isDirectory()) { 
      this.processMessage("Rules file exists and its not a directory");
      this.processMessage("Reading rules file content.");
      this.rule = this.readFileContent(this.rulefile);
      if(this.rule == "" || !this.rule.contains("|")){
        this.processMessage("Rule content empty or invalid");
        return false;
      }else{
        return true;
      }
    }else{
      this.processMessage("Rules file cannot be found or invalid");
      return false;
    }
  }
  
  private String readFileContent(String filename){
    String content = null;
       File file = new File(filename); //for ex foo.txt
       FileReader reader = null;
       try {
         reader = new FileReader(file);
         char[] chars = new char[(int) file.length()];
         reader.read(chars);
         content = new String(chars);
         reader.close();
       } catch (IOException e) {
         this.processMessage(e.getMessage());
         return "";
         //e.printStackTrace();
       } finally {
         /*if(reader !=null){
           reader.close();
         }*/
       }
       this.processMessage("Content Readed");
       this.processMessage(content);
      return (content.trim());
    
  
  }
  
  private void processMessage(String message){
    System.out.println("# "+message);
  }
  private void pauseProgram(int miliseconds){
    try {
      Thread.sleep(miliseconds);                 //1000 milliseconds is one second.
    } catch(InterruptedException ex) {
      Thread.currentThread().interrupt();
    }
  }
  private void terminateProgram(String message){
    System.out.println("##--## "+message);
  }
  
   private void pressAnyKeyToContinue(){ 
        this.processMessage("Press ENTER key to continue...");
        try
        {
            System.in.read();
        }  
        catch(Exception e)
        {}  
   }
  
}
