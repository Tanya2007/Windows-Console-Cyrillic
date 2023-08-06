#include <iostream>
#include <string>

#define UTF8_encoded_file	1			//Indicates that the source file is encoded in utf8 
							//(1 if yes, and 0 if no (i.e. if the file encoding is in ANSI)).

#if defined (_WIN32) && UTF8_encoded_file
#include <windows.h>
#include <vector>
#define _TBA UTF8_to_CP1251
std::string UTF8_to_CP1251(const std::string &utf8)
{
	if(!utf8.empty())
	{
		int wchlen = MultiByteToWideChar(CP_UTF8, 0, utf8.c_str(), -1, NULL, 0);
		if(wchlen > 0 && wchlen != 0xFFFD)
		{
			std::vector<wchar_t> wbuf(static_cast<std::size_t>(wchlen));
			MultiByteToWideChar(CP_UTF8, 0, utf8.c_str(), -1, &wbuf[0], wchlen);
			std::vector<char> buf(static_cast<std::size_t>(wchlen));
			WideCharToMultiByte(1251, 0, &wbuf[0], -1, &buf[0], wchlen, 0, 0);
			return std::string(&buf[0]);
		}
	}
	return std::string();
}

#else
#define _TBA
#endif

int main()
{
	//Example of working with Cyrillic in the Windows console, with utf-8 file encoding
	//The Cyrillic alphabet is also displayed correctly in debugging
	
#if defined (_WIN32)
	std::system("chcp 1251 > NUL");			//In the windows console, Cyrillic works only in ANSI encoding
#endif
	
	std::string ch;
	std::cout << _TBA("Привет!") << "\n";		//Convert Cyrillic alphabet from utf8 encoding to ANSI

	std::cin >> ch;					//here we enter the Cyrillic alphabet
	std::cout << ch << "\n";			//everything is output correctly
	
	char temp = ch.c_str()[0];
	
	std::string temp1 = _TBA("П");			//working with Cyrillic characters is correct only through strings
	
	if(temp1.c_str()[0] == temp)			//Comparison of Cyrillic characters is correct			
		std::cout << "Yes\n";
		
	std::cout << temp1;
	
	return 0;
}
