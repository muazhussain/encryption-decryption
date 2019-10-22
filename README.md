# encryption-decryption
Encryption is the process of translating plain text data into something that appears to be random and meaningless(ciphertext). Decryption is the process of converting ciphertext back to plaintext.
To encrypt more than a small amount of data, symmetric encryption is used. A symmetric key is used during both the encryption and decryption process. To decrypt a particular piece of ciphertext, the key that was used to encrypt the data must be used.This program uses features of object-oriented programming and file handling for better encryption and decryption system.

Program Structure:

The program consists of four steps:
	
* First it shows the menu 
* Then it get input of the string for encrypton or decryption 
* Get input of the password for encryption or decryption
* Finally shows user the output string

```

Source Code:

//*******************************//
/*   Encryption & Decrlyption   */
//*******************************//

#include<bits/stdc++.h>
using namespace std;

// Class used in the program

class encryption_decryption{
    private:
        string output_string; // For storing output string
        string input_string; // For storing input string
        string encrypt_pass; // For storing encryption passward
        string decrypt_pass; // For storing decryption passward
        int encrypt_key;
        int decrypt_key;
        int temp;
        char ch;
        void do_encryption(); // Function for encryption
        void do_decryption(); // Function for decryption
        
    public:
        encryption_decryption();
        encryption_decryption(string); // Constractor
        void set_input_string(string); // Function for setting the input string
        void set_encrypt_pass(string); // Function for setting a passward for a encrypted string
        ~encryption_decryption(); // Distracrtor
        int cheak_encrypt_pass(string); // Function for cheaking the encryption passward
        int cheak_decrypt_pass(string); // function for cheaking the decryption passward
        void get_output_string(); // Function for showing the output string
    }; // Class ends here
    
int main(){
    string string_input;
    string pass;
    encryption_decryption obj;
    
    cout << "***************************" << endl;
    cout << "  ENCRYPTION & DECRYPTION" << endl;
    cout << "***************************" << endl;
    
    bool process_continue = true;
    while(process_continue){
    cout << "\n\nMain Menu::" << endl << endl;
    cout << "1. Encryption " << endl;
    cout << "2. Decryption" << endl;
    cout << "3. Exit" << endl << endl;
    cout << "Enter Option(1-3): ";
    
        int op;
        cin >> op;
        
        switch(op){
            case 1:
                cout << "Enter the word to encrypt: ";
                cin.ignore();
                getline(cin, string_input);
                obj.set_input_string(string_input);
                cout << "Enter the passdward to set encryption: ";
                cin.ignore();
                getline(cin, pass);
                obj.set_encrypt_pass(pass);
                if(obj.cheak_encrypt_pass(pass) == 1){
                    obj.get_output_string();
                }
                else{
                    break;
                }
                break;
            case 2:
                cout << "Enter the word to decrypt: ";
                cin.ignore();
                getline(cin, string_input);
                obj.set_input_string(string_input);
                cout << "Enter the passward to proceed decrypttion: ";
                cin.ignore();
                getline(cin, pass);
                if(obj.cheak_decrypt_pass(pass) == 1){
                    obj.get_output_string();
                }
                else{
                    break;
                }
                break;
            case 3:
                cout << "Exiting the program. \nThank you for using!" << endl << endl;
                process_continue = false;
                break;
        }
    }
    return 0;
}

void encryption_decryption :: do_encryption(){
    for(int i = 0; i < input_string.size(); i++){
        temp = (int) input_string[i];
        temp += encrypt_key;
        ch = (char) temp;
        output_string += ch;
    }
}

void encryption_decryption :: do_decryption(){
    for(int i = 0; i < input_string.size(); i++){
        temp = (int) input_string[i];
        temp += decrypt_key;
        ch = (char) temp;
        output_string += ch;
    }
}

void encryption_decryption :: get_output_string(){
    output_string += '\0';
    cout << "The Encrypted/Decrypted String is: " << output_string << endl;
    output_string = "";
}

int encryption_decryption :: cheak_encrypt_pass(string pass){
    if(pass != encrypt_pass){
        cout << "Incorrect Passward! Try Again Leter." << endl;
        return 0;
    }
    else{
        do_encryption();
        return 1;
    }
}

void encryption_decryption :: set_encrypt_pass(string pass){
    fstream fio("keyfile.txt", ios::out);
    encrypt_pass = pass;
    fio << pass;
}

int encryption_decryption :: cheak_decrypt_pass(string pass){
    fstream fio("keyfile.txt", ios::in);
    string temp_pass;
    cin.ignore();
    fio >> temp_pass;
    if(temp_pass != pass){
        cout << "Incorrect Passward! Decryption will not proceed." << endl;
        return 0;
    }
    else{
        do_decryption();
        return 1;
    }
}

encryption_decryption :: encryption_decryption(){
    input_string = {""};
    output_string = {""};
    encrypt_pass = {""};
    decrypt_pass = {""};
    encrypt_key = {11};
    decrypt_key = {-1 * encrypt_key};
    temp = {};
    ch = {'\0'};
}

encryption_decryption :: encryption_decryption(string s){
    input_string = s;
}

void encryption_decryption :: set_input_string(string s2){
    input_string = s2;
}

encryption_decryption :: ~encryption_decryption(){
    }
    
