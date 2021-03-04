# racionals numbers
 my implementation for one kind of abstract data

#include <iostream>
#include <stdlib.h>
#include <cmath>
#include <cstdlib>

using namespace std;

int mmc (int a, int b); 

struct Racionais {
	public:
		Racionais (int n, int d); // inicializa o objeto com numerodor e denominador
		Racionais (int numeroInteiro); // inicializa o obheto com um numero do tipo numeroInteiro/1 (ou seja, um isomorfismo com os numero naturais)
		Racionais (); //inicializa o objeto como zero
		friend const istream& operator >> (const istream& entrada, const Racionais& numero);
		friend const ostream& operator << (const ostream& saida, const Racionais& numero); 
		friend const Racionais operator + (const Racionais& numero1, const Racionais& numero2); 
		friend const Racionais operator - (const Racionais& numero1, const Racionais & numero2);
		friend bool operator == (const Racionais& numero1, const Racionais& numero2);
		friend const Racionais operator * (const Racionais& numero1, const Racionais& numero2);
		friend const Racionais operator / (const Racionais& numero1, const Racionais& numero2);
		void teste (void);
		
		
	private:
		int numerador;
		int denominador;
		void sinal_racional(); // implementa o sinal do numero  racional a partir dos numeros inteiros
		void numero_racional(); // transforma o numero racional em fracao irredutivel, se for necessario
};

int main () {
	
	Racionais a(5,2);
	Racionais b(15,6);
	cout << a;
	cout << "\n";
	
	cout <<"Soma \n" << a+b ;
	cout << "\n";
	
	
  if (a == b ) {
  	cout << "Os numeros sao iguais\n";
  }	 
  
  else {
  	
  	cout << "os numeros sao diferentes\n";
  }
	
	
	
	return 0;
}




Racionais::Racionais() {
		int numerador = 0;
		int denominador = 1; }

Racionais::Racionais(int n, int d) {
	numerador = n;
	denominador = d;
	while (d==0) {
		cout << " O denominador nao pode ser nulo\n" << "Entre com o novo denominador\n";
		cin >> denominador;
		}
	sinal_racional(); // atua no objeto construído pelo construtor. Essa funçao só pode ser chamada assim como uma rotina de um construtor caso contrário, em que objeto ela atuaria???
	numero_racional();
		 }

Racionais::Racionais(int numeroInteiro) {
	numerador = numeroInteiro;
	denominador =  1;
}

const istream& operator >> (const istream& entrada, const Racionais& numero) {
	cin >> numero.numerador;
	cin >> numero.denominador;

	return entrada;
}
	
	
	

const ostream& operator << (const ostream& saida, const Racionais& numero) {
	cout << numero.numerador <<"/" ;
	cout << numero.denominador;
	return saida;
	
	}
void Racionais::sinal_racional () {
	if (((numerador <0) && (denominador <0)) || ((numerador>0) && (denominador <0))) { 
		numerador = -1*numerador;
		denominador = -1*denominador;
	}}


void Racionais::numero_racional () {
	int x = mmc (6,7);
	int i = numerador;
	while (i > 1) {
		if ((numerador%i ==0) && (denominador%i ==0)){
			numerador = numerador/i;
			denominador = denominador/i;
			 }
		i = i-1; }}
		
const Racionais operator + (const Racionais& numero1, const Racionais& numero2) { // as funçoes amigas nao tem acesso às funçoes privadas da classe;

	int a = numero1.denominador;
	int b = numero2.denominador;
	int denominador_soma = numero1.denominador*numero2.denominador;
	return Racionais (numero1.numerador*numero2.denominador + numero1.denominador*numero2.numerador, denominador_soma);
	
} 

const Racionais operator - (const Racionais& numero1, const Racionais& numero2) {
	int denominador_subtracao = numero1.denominador*numero2.denominador;
	return Racionais (numero1.numerador*numero2.denominador - numero1.denominador*numero2.numerador  , denominador_subtracao);
	
} 


int mmc (int a, int b) {
	int mmc_resultado = a; // também poderia ser mmc = b
	
	while (true) {
	if ((mmc_resultado%a ==0) && (mmc_resultado%b ==0)) {
		return mmc_resultado;
		}
		mmc_resultado = mmc_resultado +1; }}
		

bool operator == (const Racionais& numero1, const Racionais& numero2) {
	return numero1.numerador*numero2.denominador == numero2.numerador*numero1.denominador; }
	
const Racionais operator * (const Racionais& numero1, const Racionais& numero2) {
	int numerador_produto = numero1.numerador*numero2.numerador;
	int denominador_produto = numero1.denominador*numero2.denominador;
	
	return Racionais (numerador_produto, denominador_produto);
}

const Racionais operator / (const Racionais& numero1, const Racionais& numero2 ) {
	
	return Racionais (numero1.numerador*numero2.denominador, numero1.denominador*numero2.numerador); }