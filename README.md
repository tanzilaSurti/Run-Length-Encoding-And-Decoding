# Run-Length-Encoding-And-Decoding

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
namespace DS_lab
{

    class Program
    {
        public static string RunlengthEncode(string input)
        {
            string encodevalue = "";
            int i = 0;
            int count = 1;
            input = input + "";
            for (i = 0; i < input.Length; i++)
            {
                if (i + 1 < input.Length && input[i] == input[i + 1])
                {
                    count++;
                }
                else
                {
                    encodevalue = encodevalue + input[i];
                    encodevalue = encodevalue + count;
                    count = 1;
                }
            }
            Console.WriteLine("input: "+input);
            Console.WriteLine("Encoded string: " +encodevalue+"\n\n");
            return encodevalue;
        }

        public static string runlengthdecode(string s)
        {
            string decoded_value="";
            for (int i = 0; i < s.Length; i=i+2)
            {
                char a = s[i];
                int num = (int)Char.GetNumericValue(s[i + 1]);
                
                for (int j = 0; j < num; j++)
                {
                    decoded_value += a;
                }
            }
            Console.WriteLine("Input : "+s);
            Console.WriteLine("Decoded String: "+decoded_value+"\n\n");
            return decoded_value;
        }
        static void Main(string[] args)
        {
             string encoded_string;
             string input;
             string path = @"C:\Users\tanzila\Desktop\input.txt";
             string output_path = @"C:\Users\tanzila\Desktop\encode.txt";
             string decode_value_output_path = @"C:\Users\tanzila\Desktop\decode.txt";
             StreamReader sr = new StreamReader(path);
           
             StreamWriter sw = new StreamWriter(output_path);          
             if(!File.Exists(path)){
                   Console.WriteLine("File not Found");
             }
             else{                 
                 while(sr.Peek()>-1){
                    
                     input = sr.ReadLine();
                     encoded_string=RunlengthEncode(input);
                     sw.WriteLine(encoded_string);
                 }
             }
             sw.Close();
             sr = new StreamReader(output_path);         //Opening encoded output file for reading
                    //creating a new file for decoding output
             sw = new StreamWriter(decode_value_output_path);
             if (!File.Exists(output_path))
             {
                 Console.WriteLine("File Does not Found");
             }
             else
             {
                 while (sr.Peek() > -1)
                 {
                     string line = sr.ReadLine();
                     string decoded_string = runlengthdecode(line);
                     sw.WriteLine(decoded_string);
                 }
             }
           
             sw.Close();            
             Console.ReadLine();
        }
    }
}

