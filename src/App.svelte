<script>
import Kofi from "./kofi.svelte";
let thaiengInput;
let engthaiInput;
let thaiengResult = '';
let engthaiResult = '';

const dictEngToTh = {
  "1"   : "ๅ",  
  "`"   : "_",  
  "2"   : "/",  
  "3"   : "-",  
  "4"   : "ภ",  
  "5"   : "ถ",  
  "6"   : "ุ",  
  "7"   : " ึ",  
  "8"   : "ค",  
  "9"   : "ต",  
  "0"   : "จ",  
  "-"   : "ข",  
  "="   : "ช",  
  "q"   : "ๆ",  
  "w"   : "ไ",  
  "e"   : "ำ",  
  "r"   : "พ",  
  "t"   : "ะ",  
  "y"   : "ั",  
  "u"   : "ี",  
  "i"   : "ร",  
  "o"   : "น",  
  "p"   : "ย",  
  "["   : "บ",  
  "]"   : "ล",  
  "\\"  : "ฃ",  
  "a"   : "ฟ",  
  "s"   : "ห",  
  "d"   : "ก",  
  "f"   : "ด",  
  "g"   : "เ",  
  "h"   : "้",  
  "j"   : "่",  
  "k"   : "า",  
  "l"   : "ส",  
  ";"   : "ว",  
  "\'"  : "ง",  
  "z"   : "ผ",  
  "x"   : "ป",  
  "c"   : "แ",  
  "v"   : "อ",  
  "b"   : "ิ",  
  "n"   : "ื",  
  "m"   : "ท",  
  ","   : "ม",  
  "."   : "ใ",  
  "\/"  : "ฝ",  
  
  "~"   : "%",  
  "!"   : "+",  
  "@"   : "๑",  
  "#"   : "๒",  
  "$"   : "๓",  
  "%"   : "๔",  
  "^"   : "ู",  
  "&"   : "฿",  
  "*"   : "๕",  
  "("   : "๖",  
  ")"   : "๗",  
  "_"   : "๘",  
  "+"   : "๙",  
  "Q"   : "๐",  
  "W"   : "\"",
  "E"   : "ฎ",  
  "R"   : "ฑ",  
  "T"   : "ธ",  
  "Y"   : "ํ",  
  "U"   : "๊",  
  "I"   : "ณ",  
  "O"   : "ฯ",  
  "P"   : "ญ",  
  "{"   : "ฐ",  
  "}"   : ",",  
  "\|"  : "ฅ",  
  "A"   : "ฤ",  
  "S"   : "ฆ",  
  "D"   : "ฏ",  
  "F"   : "โ",  
  "G"   : "ฌ",  
  "H"   : "็",  
  "J"   : "๋",  
  "K"   : "ษ",  
  "L"   : "ศ",  
  ":"   : "ซ",  
  "\""  : ".",  
  "Z"   : "(",  
  "X"   : ")",  
  "C"   : "ฉ",  
  "V"   : "ฮ",  
  "B"   : "ฺ",  
  "N"   : "์",  
  "M"   : "?",  
  "<"   : "ฒ",  
  ">"   : "ฬ",  
  "?"   : "ฦ",
  " "   : " ",
  "\n"  : "\n",
  "\r"  : "\r"
}  
                                          
const dictThToEng = {
  "_"   :  "`" ,                 
  "ๅ"   :  "1" ,                 
  "/"   :  "2" ,                
  "-"   :  "3" ,                
  "ภ"   :  "4" ,                
  "ถ"   :  "5" ,                
  "ุ"    :  "6" ,                
  " ึ"   :   "7" ,                
  "ค"   :  "8" ,                
  "ต"   :  "9" ,               
  "จ"   :  "0" ,                 
  "ข"   :  "-" ,                
  "ช"   :  "=" ,                
  "ๆ"   :  "q" ,                
  "ไ"   :  "w" ,               
  "ำ"   :  "e" ,                
  "พ"   :  "r" ,               
  "ะ"   :   "t" ,             
  "ั"    :   "y" ,               
  "ี"    :  "u" ,                
  "ร"   :   "i" ,             
  "น"   :  "o" ,                  
  "ย"   :  "p" ,                
  "บ"   :  "[" ,                
  "ล"   :  "]" ,                
  "ฃ"   :  "\\",                
  "ฟ"   :  "a" ,                
  "ห"   :  "s" ,                
  "ก"   :  "d" ,                
  "ด"   :  "f" ,                
  "เ"   :   "g" ,               
  "้"    :   "h" ,               
  "่"    :   "j" ,               
  "า"   :   "k" ,               
  "ส"   :   "l" ,               
  "ว"   :   ";" ,               
  "ง"   :   "\'",               
  "ผ"   :   "z" ,               
  "ป"   :   "x" ,               
  "แ"   :   "c" ,               
  "อ"   :   "v" ,               
  "ิ"    :   "b" ,               
  "ื"    :   "n" ,               
  "ท"   :   "m" ,               
  "ม"   :   "," ,               
  "ใ"   :   "." ,               
  "ฝ"   :   "\/",               
                            
  "%"   :    "~",              
  "+"   :    "!",              
  "๑"   :    "@" ,              
  "๒"   :    "#" ,              
  "๓"   :    "$" ,              
  "๔"   :    "%" ,              
  "ู"    :    "^" ,              
  "฿"   :    "&" ,              
  "๕"   :    "*" ,              
  "๖"   :    "(" ,              
  "๗"   :    ")" ,              
  "๘"   :    "_" ,              
  "๙"   :    "+" ,              
  "๐"   :    "Q" ,              
  "\""  :    "W" ,                
  "ฎ"   :    "E" ,              
  "ฑ"   :    "R" ,              
  "ธ"   :    "T" ,              
  "ํ"    :    "Y" ,              
  "๊"    :    "U" ,              
  "ณ"   :    "I" ,              
  "ฯ"   :    "O" ,              
  "ญ"   :    "P" ,              
  "ฐ"   :    "{" ,              
  ","   :    "}" ,              
  "ฅ"   :    "\|",              
  "ฤ"   :    "A" ,              
  "ฆ"   :    "S" ,              
  "ฏ"   :    "D" ,               
  "โ"   :    "F" ,              
  "ฌ"   :   "G" ,               
  "็"    :    "H" ,              
  "๋"    :    "J" ,              
  "ษ"   :   "K" ,              
  "ศ"   :    "L" ,              
  "ซ"   :   ":" ,               
  "."   :   "\"",                
  "("   :   "Z" ,               
  ")"   :   "X" ,               
  "ฉ"   :   "C" ,               
  "ฮ"   :   "V" ,               
  "ฺ"    :   "B" ,               
  "์"    :   "N" ,               
  "?"   :   "M" ,               
  "ฒ"   :   "<" ,               
  "ฬ"   :   ">" ,               
  "ฦ"   :   "?",
  " "   : " ",
  "\n"  : "\n"  
}               

const engthaiswap = () => {
  let swappedText = engthaiInput.replace(/ 1|2|3|4|5|6|7|8|9|0|-|=|q|w|e|r|t|y|u|i|o|p|[|]|\\|a|s|d|f|g|h|j|k|l|;|\'|z|x|c|v|b|n|m|,|.|\/|!|@|#|\$|%|\^|&|\*|\(|\)|_|\+|Q|W|E|R|T|Y|U|I|O|P|\{|\}|\\|\||A|S|D|F|G|H|J|K|L|:|\"|Z|X|C|V|B|N|M|<|>|\?|`|~|\n|\r /g, function(char) {
    console.log(dictEngToTh[char])
    return dictEngToTh[char]
  });

  if (swappedText.includes("undefined")) {
    engthaiResult = "กรุณาใส่เฉพาะตัวอักษรภาษาอังกฤษ" 
  } else {
    engthaiResult = swappedText;
  }
};

const thaiengswap = () => {
  let swappedText = thaiengInput.replace(/ ๅ|\/|-|ภ|ถ|ุ|ึ|ค|ต|จ|ข|ช|ๆ|ไ|ำ|พ|ะ|ั|ี|ร|น|ย|บ|ล|ฃ|ฟ|ห|ก|ด|เ|้|่|า|ส|ว|ง|ผ|ป|แ|อ|ิ|ื|ท|ม|ใ|ฝ|\+|๑|๒|๓|๔|ู|฿|๕|๖|๗|๘|๙|๐|"|ฎ|ฑ|ธ|ํ|๊|ณ|ฯ|ญ|ฐ|,|ฅ|ฤ|ฆ|ฏ|โ|ฌ|็|๋|ษ|ศ|ซ|\.|\(|\)|ฉ|ฮ|ฺ|์|\?|ฒ|ฬ|ฦ|_|%\n|\r /g, function(char) {
    console.log(dictThToEng[char])
    return dictThToEng[char]
  });
  
  if (swappedText == thaiengInput) {
    thaiengResult = "กรุณาใส่เฉพาะตัวอักษรภาษาไทย" 
  } else {
    thaiengResult = swappedText;
  }
};
</script>

<style>

  @import url('https://fonts.googleapis.com/css2?family=PT+Sans&display=swap');

  :root {
    background-color: #282a36;
    overflow: hidden;
    text-align: center;
    padding: 10px;
  }
  
  h1 {
    color: #bd93f9;
    font-family: "PT Sans";
    font-size: 2rem;
  }

  h2 {
    color: #8be9fd;
    font-family: "PT Sans";
    font-size: 2rem;
  }

  input {
    color: #f1fa8c;
    background-color: #44475a00;
    border-color: #44475a00;
    font-size: 2rem;
    outline: none;
    border-bottom: 3px solid #44475a;
    max-width: 50%;
  }
  
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  
  button {
    background-color: #ff5555	;
    border: 0px;
    color: #f8f8f2;
    padding: 10px;
  }

  .row {
    display: flex;
  }

  .column {
    flex: 50%;
  }

  .line {
    border-right: thick solid #ff5555		;
  }

  @media screen and (max-width: 600px) {
  :root{
    text-align:center;
    padding: 0px;
  }

  input {
    font-size: 1rem;
    width: 100%;
    max-width: 100%;
    text-align:center;
  }

  h1 {
    font-size: 1.2rem;
  }  

  h2 {
    font-size: 1rem;
  }
  
  .line {
    border-bottom: thick solid #ff5555		;
  }

  .row {
    display: block;
  }
  
  button {
    padding: 10px;
  }

  }

</style>

<Kofi name="sleepysheeep" />

<center>
  <h1>Thai-Eng Swap</h1>
  <div class="row">
    <div class="column" style="">
      <h2>de => กำ</h2>
      <input bind:value={engthaiInput}  type="text"><br>
      <button on:click="{engthaiswap}">Submit</button>
      <h2>{engthaiResult}</h2>
    </div><br>
    <div class="line"></div>
    <div class="column" style="">
      <h2>กำ => de</h2>
      <input bind:value={thaiengInput}  type="text"><br>
      <button on:click="{thaiengswap}">Submit</button>
      <h2>{thaiengResult}</h2>
    </div>
  </div>
</center>
