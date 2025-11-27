#include <iostream>
#include <string>
#include <fstream>
#include <vector>
#include <sstream>
#include <iomanip>
using namespace std;
struct Mish
{
	int ves;
	string firma;
	string ind;
};
int One(const Mish* m, int MishVes) {
	int MaxVes = 0;
	int MaxInd = 0;
	for (int i = 0; i < MishVes; i++) {
		if (m[i].ves > MaxVes) {
			MaxVes = m[i].ves;
			MaxInd = i;
		}
	}
	return MaxInd;
}
int main() {
	setlocale(LC_ALL, "RUS");
	Mish num1 = { 150,"bloody","chine" };
	Mish* ptr = &num1;
	cout << "вес товара:" << ptr->ves << endl << "фирма производителя:" << ptr->firma << endl << "индекс товара:" << ptr->ind << endl;
	Mish* m = new Mish[3];
	m[0] = { 150,"bloody","238556" };
	m[1] = { 200,"bloody","745656" };
	m[2] = { 57,"Dell","43534" };
	int maxInd=One(m, 3);
	cout << m[maxInd].ind << endl;
	delete[] m;


	ofstream fmish("mish.txt");
	fmish << "150 bloody 238556\n";
	fmish << "200 bloody 745656\n";
	fmish << "57 Dell 43534\n";
	fmish.close();
	ifstream infmish("mish.txt");
	vector<Mish> MishVector;

	Mish asb;
	while (infmish >> asb.ves >> asb.firma >> asb.ind) {
		MishVector.push_back(asb);
	}
	infmish.close();

	cout << "\n таблица:" << endl;
	cout << "|" << setw(5) << "вес"<< "|" << "фирма"<<"|"<< "индекс" << endl;
	for (const auto& it : MishVector) {
		cout << "|" << setw(5) << it.ves << "|" << setw(15) << it.firma << "|" << setw(15) << it.ind << "|" << endl;
	}
	stringstream ss;
	for (const auto& it : MishVector) {
		ss << "вес-" << it.ves << endl;
		ss << "фирма-" << it.firma << endl;
		ss << "индекс-" << it.ind << endl;
	}
	ofstream DoubleMish("Double_Mish.bin", ios::binary);
	string data = ss.str();
	DoubleMish.write(data.c_str(), data.size());
	DoubleMish.close();
	return 0;
}








