#include<iostream>
#include<cmath>
#include<numeric>
#include<vector>
#include<string>
using namespace std;
 
int gcd(int a , int b){
    if (a == 0)
        return b;
    return gcd(b % a, a);
}
 
int getP(int n){
    int p;
    int num1 = sqrt(n);
    int num2;
 
    while(num1 != 0){
        if(n%num1 == 0){
            num2 = n / num1;
            int GCD = gcd(num1, num2);
            if(GCD == 1){
                p = num1;
                return p;
            }
        }
        num1 = num1 - 1;
    }
    return p;
}
 
int getD(int e, int u){
    int d; 
 
    int coefficient = 1;
    int temp = u +1;
 
    while(temp%e != 0){
        coefficient = coefficient +1;
        temp = (u * coefficient) +1;
    }
 
    d = temp / e;
 
    return d;
}
 
int decode(int inVec, int d, int n){
    int solution;
 
    int reserve = 1;
    int base = inVec;
 
    while(d!= 2){
        if(d%2 != 0){
            reserve = reserve * base;
            d = d-1;
        }
        base = pow(base, 2);
        base = base % n;
        d = d/2;
 
        if(d == 1){
            int final1 = reserve % n;
            int final2 = base;
            final2 = final2 % n;
 
            solution = final1 * final2;
            solution = solution % n;
 
            return solution;   
        }
    }
 
    int final1 = reserve % n;
    int final2 = pow(base, 2);
    final2 = final2 % n;
 
    solution = final1 * final2;
    solution = solution % n;
 
    return solution;
}
 
bool check(int letter){
    for(int i = 2; i < letter; i ++){
        if(letter%i == 0){
            return false;
        }
    }
    return true;
}
 
int main(){
    int e, n, m;
    cin >> e;
    cin >> n;
    cin >> m;
 
    if(m == 0){
        return 0;
    }
 
    vector<int> encoded;
 
    int temp;
    for(int i = 0; i < m; i++){
        cin >> temp;
        encoded.push_back(temp);
    }
 
    int GCD = gcd(e, n);
    if(GCD != 1 || e == n){
        cout << "Public key not valid!";
        return 0;
    }
    else if(e < 1 || e > n){
        cout << "Public key not valid!";
        return 0;
    }
 
    int p = getP(n);
    int q = n/p;
 
    if(p == q || n == p){
        cout << "Public key not valid!";
        return 0;
    }
    else if(n==q){
        cout << "Public key not valid!";
        return 0;
    }
    bool checkP = check(p);
    bool checkQ = check(q);
 
    if(!checkP || !checkQ){
        cout << "Public key not valid!";
        return 0;
    }
 
    int GCD2 = gcd(p, q);
    if(GCD2 != 1 || p*q != n){
        cout << "Public key not valid!";
        return 0;
    }
 
    int u = (q-1) * (p-1); // this is phi(n)
    int d = getD(e, u);
 
    if(1 >= d || d > n){
        cout << "Public key not valid!";
        return 0;
    }
    int GCD3 = gcd(e, u);
    if(GCD2 != 1){
        cout << "Public key not valid!";
        return 0;
    }
 
    int temp1 = d*e;
    temp1 = temp1%u;
    if(temp1 != 1){
        cout << "Public key not valid!";
        return 0;
    }
 
    // int temp2 = e % u;
    // if(1/d != temp2){
    //     cout << "Public key not valid!";
    //     return 0;
    // }
 
    vector<int> decoded;
 
    for(int i = 0; i < m; i++){
        int newNum = decode(encoded.at(i), d, n);
        decoded.push_back(newNum);
    }
 
    vector<char>translate;
    char letter = 'A';
    for(int i = 0; i < 26; i++){
        translate.push_back(letter);
        letter = letter +1;
    }
 
    translate.push_back(' ');
    translate.push_back('"');
    translate.push_back('.');
    translate.push_back(',');
    translate.push_back('\'');
 
    vector<char>message;
    for(int i = 0; i < m; i++){
        char input = translate.at(decoded.at(i) - 3);
        message.push_back(input);
    }
 
    cout << p << " " << q << " " << u << " " << d << endl;
    for(int i = 0; i < m; i++){
        cout << decoded.at(i) << " ";
    }
    cout << endl;
 
    for(int i = 0; i < m; i++){
        cout << message.at(i);
    }
 
 
    return 0;
}
