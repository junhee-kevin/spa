#include <stdio.h> 
#include <stdlib.h> 
#include <time.h> 
#include <math.h>

double random(); 
int possion();

double random() {	
	double f;
	srand((unsigned)time(NULL));
	f = (float)(rand() % 100);
	
	return f/100;
}

int possion(int lamda) {
	
	int P=0; 
	long double  B = exp(-lamda); // l 은 e의 -lamda 승 
	long double PROD = 1.0;

	while (PROD >= B) {
		double ran = random(); 
		//printf("%f\n", ran);
		PROD = PROD * ran;
		P = P + 1;
	}
	return P - 1; 
}
//
//int main(void) {
	//printf("%f\n", random());
//	for (int i = 0; i < 100; i++) {
//		printf("%d\n", possion(4));
//	}
//}
int main(void) {
	double queue = 0; 
	double totque = 0;
	double tpump = 0;
	double time = 0;
	double tstep = 1.0;
	double arrive = 0;
	double aveque = 0;
	double prarr = 0.3;
	double tlimit = 100.0;

	while (time < tlimit) {
		time = time + tstep; 
		arrive = 0; 
		double u = random(); 
		if (u < prarr * tstep) {
			arrive = arrive + 1;
			queue = queue + arrive; 
		}
		if (tpump > 0) {
			tpump = tpump - tstep;
			if (tpump < 0) {
				tpump = 0; 
			}
		}
		if (tpump == 0 && queue != 0) {
			queue = queue - 1; 
			int e = possion(4);
			tpump = e;
		}
		totque = totque + queue; 
		aveque = totque / (tlimit / tstep); 

		printf("%f\n", time);
		printf("%f\n", arrive);
		printf("%f\n", queue);
		printf("%f\n", tpump);

		printf("%f\n", totque);
		printf("%f\n", aveque);
		printf("\n");
	}


	
}
