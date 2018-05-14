# name.cpp
///Implementación de la clase Name
#include "name.h"

using namespace std;

///Constructor base
Name::Name() {
    last = "NULL";
    first = "NULL";
}

Name::Name(const Name&n) : last (n.last), first(n.first) { } ///Constructor copia

Name::Name(const std::string&l, std::string&f) : last(l), first(f){ }///Constructor parametrizado

string Name::getLast() {
    return last;
    }

string Name::getFirst() {
    return first;
    }

void Name::setLast(const std::string&l) {
    last = l;
    }

void Name::setFirst(const std::string&f) {
    first = f;
    }

string Name::toString() {
    return last + " " + first;
    }

bool Name::isName(Name& myName){
    int tam = 0;
    bool flag = true;
    string aux;

    ///Extrae los nombres en una auxiliar
    aux = myName.getFirst();
    aux += myName.getLast();

    tam = aux.size();   ///Checa tamaño de la auxiliar

    ///Checa si un caracter no coincide con el alfabeto
    for(int i = 0; i < tam; i++){
        ///Si no coincide, la cadena es inválida
        if(!isalpha(aux[i])){
            flag = false;
        }
    }

    ///si es un nombre válido lo actualiza a mayusculas
    if(flag){
        tam = last.size();
        for(int i = 0; i < tam; i++){
            last[i] = toupper(last[i]);
        }
        tam = first.size();
        for(int i = 0; i < tam; i++){
            first[i] = toupper(first[i]);
        }
    }

    return flag;
}

/*** Sobrecarga de operadores ***/
Name& Name::operator = (const Name&n) {
    last = n.last;
    first = n.first;
    return *this;
    }

bool Name::operator == (Name&n) {
    if(last == n.last and first == n.first){
        return toString() == n.toString();
    }
    else{
        return false;
    }
}

bool Name::operator != (Name&n) {
    if( last != n.last and first != n.first){
        return this->toString() != n.toString();
    }
    else{
        return false;
    }
}

bool Name::operator < (Name&n) {
    if( last < n.last and first < n.first){
        return toString() < n.toString();
    }
    else{
        return false;
    }
}

bool Name::operator <= (Name&n) {
    if( last <= n.last and first <= n.first){
        return toString() <= n.toString();
    }
    else{
        return false;
    }
}

bool Name::operator>(Name&n) {
    if( last > n.last and first > n.first){
        return toString() > n.toString();
    }
    else{
        return false;
    }
}

bool Name::operator >= (Name&n) {
    if( last >= n.last and first >= n.first){
        return toString() >= n.toString();
    }
    else{
        return false;
    }
}

ostream& operator << (ostream& os, Name&n){
    os << n.toString();
    return os;
}

istream& operator >> (istream&is, Name&n)
{
    string myStr;
    getline(is, myStr,'-');
    n.last = myStr;

    getline(is,myStr,'\n');
    n.first = myStr;
    return is;
}
