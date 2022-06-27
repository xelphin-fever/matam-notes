# C++
# 📂 Ofstream and Instream

## What are the Ofstream and Ifstream?

```Ofstream``` **writes** into file. ```Ifstream``` **reads** a file.

```cpp
#include <fstream>
using std::ifstream;
using std::ofstream;
using std::cerr;
using std::endl;
```
```cpp
void copyFile(const char* sourceFileName, const char* targetFileName) {

  // file that you are reading from
	ifstream source(sourceFileName);

  // checks if you couldn't open file
	if (!source) { 
		cerr << "cannot open file " << sourceFileName << endl;
		return; // don't need to clode because d'tor auto called
  }

  // file that you are writing into
	ofstream target(targetFileName);

  // Checks if you've managed to open file
	if (!target) {
		cerr << "cannot open file " << targetFileName << endl;
		return;
  }

  // tells you if you've reached end of file
	while (!source.eof()) {
		char c;
		source.get(c); // GET - put value into 'c'
		target.put(c); // PUT - place 'c' into target
  }
}
```


```cpp
#include <fstream>
#include <string>
using std::ifstream;
using std::ofstream;
using std::cerr;
using std::endl;
using std::string;
```
```cpp
void  saveSet(const Set& s, string targetFileName){
      ofstream target(targetFileName);
      if (!target) {
         // ...
    		 // Cannot open output file
       }
      for (int value : s) {
        target << value  << endl;
      }
}

Set loadSet(string sourceFileName){
      ifstream source(sourceFileName);
      if (!source) {
    		 // Cannot open input file
      }
      Set newSet;
      char line[256];
      while (source.getline(line, sizeof(line))) {
         newSet.add(std::stoi(line));	
      }
      return newSet;
}
```