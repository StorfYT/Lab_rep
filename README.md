#include <iostream>
#include <vector>
#include <string>
#include <fstream>
#include <sstream>
#include <iomanip>

using namespace std;

struct Mish {
    int ves;
    string firma;
    string ind;
};

void readFromFile(const string& filename, vector<Mish>& data) {
    ifstream fin(filename);
    if (!fin) {
        cerr << "Error opening file!" << endl;
        return;
    }
    Mish tmp;
    while (fin >> tmp.ves >> tmp.firma >> tmp.ind) {
        data.push_back(tmp);
    }
    fin.close();
}

void printData(const vector<Mish>& data) {
    cout << "\nTable:" << endl;
    cout << "|" << setw(5) << "Weight" 
         << "|" << setw(15) << "Company" 
         << "|" << setw(15) << "Index" << "|" << endl;
    for (const auto& item : data) {
        cout << "|" << setw(5) << item.ves 
             << "|" << setw(15) << item.firma 
             << "|" << setw(15) << item.ind << "|" << endl;
    }
}

void writeBinary(const string& filename, const vector<Mish>& data) {
    stringstream ss;
    for (const auto& item : data) {
        ss << "weight-" << item.ves << "\n";
        ss << "company-" << item.firma << "\n";
        ss << "index-" << item.ind << "\n";
    }
    ofstream fout(filename, ios::binary);
    string str = ss.str();
    fout.write(str.c_str(), str.size());
    fout.close();
}

int main() {
    ofstream fmish("mish.txt");
    fmish << "150 bloody 238556\n";
    fmish << "200 bloody 745656\n";
    fmish << "57 Dell 43534\n";
    fmish << "120 HP 99887\n";
    fmish << "250 Lenovo 112233\n";
    fmish << "75 Asus 556677\n";
    fmish.close();

    vector<Mish> data;
    readFromFile("mish.txt", data);
    printData(data);
    writeBinary("Double_Mish.bin", data);

    return 0;
}


