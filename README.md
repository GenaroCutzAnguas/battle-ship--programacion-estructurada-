# battle-ship--programacion-estructurada-
juego de battle ship segundo semestre 
*juego por alumnos de la UADY*

aqui te presentamos el archivo del juego 


y el codigo es:
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <conio.h>
int ganador(int campo[10][10], int campo_2[10][10], int turnos);
void imprimir_pantalla_espectro(int campo[][10]);
void imprime(int tablero_partiaccipante[][10]);
int main(){
	//Variables del juego que se vayan necesitando a lo largo del juego
	int pidbote;
	int vertical_horizontal;
	int contador_jugador = 0;
	int x,y;
	
	
	//Modulo de salve
	//Este modulo es hecho para salvar las cordenadas y horientaciones de los barcos
	//Primer jugador
	int acorazado[2];
	int artillero_1[2];
	int artillero_2[2];
	int bote[2];
	
	//Segundo jugador
	int acorazado_jo2[2];
	int artillero_1_jo2[2];
	int artillero_2_jo2[2];
	int bote_jo2[2];
	
	//Modulo de campos
	int campo[10][10];
	int campo_2[10][10];
	
	//Variables de puntos claves
	int bonos, conteo=0;
	int phil, columbo;
	
	//Modulo de generacion de campo de primer jugador
	for(int i = 0; i < 10; i++){
		for(int j = 0; j < 10; j++){
			campo[i][j] = 0;
		}
	}
	
	//Modulo de generacion de campo del segundo jugador
	for(int i = 0; i < 10; i++){
		for(int j = 0; j < 10; j++){
			campo_2[i][j] = 0;
		}
	}
	
	//Modulo de generacion de puntos clave
	//Definir cuantos puntos clave se van a crear
	bonos=rand()%4;
	
	//Ubicar los puntos clave para el jugador 1
	/*Simbología para todos los puntos claves o no
	0 = No hay  barco 
	1 = Hay un punto de un barco
	2 = Diste a un barco
	3 = Tienes disparo doble
	4 = Puedes bombardear fila
	5 = Puedes recuperar un barco*/
	 
	//Modulo para tiros dobles

	while(conteo<bonos){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo[phil][columbo]!=1 && campo[phil][columbo]!=2){
			campo[phil][columbo]=3;
			conteo++;
		}
	}

	conteo = 0;
	while(conteo<bonos){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo_2[phil][columbo]!=1 && campo_2[phil][columbo]!=2){
			campo_2[phil][columbo]=3;
			conteo++;
		}
	}

	/*Modulos para bombardear filas*/
	conteo = 0;
	while(conteo<1){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo[phil][columbo]!=1 && campo[phil][columbo]!=2 && campo[phil][columbo]!=3){
			campo[phil][columbo]=4;
			conteo++;
		}
	}

	conteo = 0;
	while(conteo<1){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo_2[phil][columbo]!=1 && campo_2[phil][columbo]!=2 && campo_2[phil][columbo]!=3){
			campo_2[phil][columbo]=4;
			conteo++;
		}
	}
	//------------------------------------------------------------------
	//Modulo de generacion de barcos 
	
	do
	{
		
		printf("\n*********************************battle ship********************\n");
		printf("Bienvenido jugador en esta seccion introduciras la generacion de tus barcos");
		printf("\nTen en cuenta que los mismos se podran encimar asi que ten cuidado de donde los pones");
		printf("\nHay limitantes para la generacion de barcos siendo: \nArtilleros y Bote solo pueden ir en vertical \nAcorazdo solo puede ir horizontal");
		printf("\naqui te presentamos un ejemplo visual del mapa que se usara:");
		//Modulo de generacion de acorazado
		
		if(contador_jugador == 0){
			imprime(campo);
			//Acorazado
			printf("\nAcorazado :");
			printf("\nSelecciona la coordenada donde se iniciara la generacion de izquierda derecha\nNOTA: ten en cuenta que el acorazado solo puede estar en columnas menores a 5");
			printf("\nEscribe la fila: ");
			scanf("%d", &acorazado[0]);
			printf("\nEscribe la columna: ");
			scanf("%d", &acorazado[1]);
			for(int i = acorazado[1]; i <= acorazado[1]+5; i++){
				campo[acorazado[0]][i] = 1;
			}
			imprime(campo);
			//Artillero 1
			printf("\nPrimer artillero: ");
			printf("\nSelecciona la coordenada donde se iniciara la generacion del primer artillero de arriba hacia abajo \nNOTA: ten en cuenta que el artillero solo puede estar en filas menores a 8");
			printf("\nEscribe la fila: ");
			scanf("%d", &artillero_1[0]);
			printf("\nEscribe la columna: ");
			scanf("%d", &artillero_1[1]);
			for(int i = artillero_1[1]; i <= artillero_1[1]+3; i++){
				campo[i][artillero_1[0]] = 1;
			}
			imprime(campo);
			
			//Artillero 2
			printf("\nSegundo artillero: ");
			printf("\nEscribe las coordenadas en donde va a ir el segundo artillero: ");
			printf("\nEscribe la fila: ");
			scanf("%d", &artillero_2[0]);
			printf("\nEscribe la columna: ");
			scanf("%d", &artillero_2[1]);
			for(int i = artillero_2[1]; i <= artillero_2[1]+3; i++){
				campo[i][artillero_2[0]] = 1;
			}
			imprime(campo);
		
			// Bote 
			printf("\nBote");
			printf("\nEscribe las coordenadas en donde va a ir el bote , iniciando la generacion de arriba a abajo \n recuerda que ubicarlo en filas menores a 8");
			printf("\nEscribe la fila: ");
			scanf("%d", &bote[0]);
			printf("\nEscribe la columna :");
			scanf("%d", &bote[1]);
			for(int i = bote[1]; i <= bote[1]+1; i++){
				campo[i][bote[0]] = 1;
			}
			imprime(campo);
			getch();
			system("cls");
			printf("la pantalla ha sido borrada, para iniciar el tuurno del siguiente jugador \n evita que el jugador 1 observe donde ubicaste tus barcos \n haz click para iniciar");
			getch();
		}
		else if (contador_jugador == 1)
		{
			//se limpia la pantalla
			imprime(campo_2);
			printf("\nTurno del jugador 2");
			printf("\nAcorazado :");
			printf("Selecciona la coordenada donde se iniciara la generacion de izquierda derecha \nNOTA: ten en cuenta que el artillero solo puede estar en columnas menores a 5");
			printf("\nEscribe la fila: ");
			scanf("%d", &acorazado_jo2[0]);
			printf("\nEscribe la columna: ");
			scanf("%d", &acorazado_jo2[1]);
			for(int i = acorazado_jo2[1]; i <= acorazado_jo2[1]+5; i++){
				campo_2[acorazado_jo2[0]][i] = 1;
			}
			imprime(campo_2);

			//Artillero 1
			printf("\nPrimer artillero: ");
			printf("\nSelecciona la coordenada donde se iniciara la generacion del primer artillero de arriba hacia abajo \nNOTA: ten en cuenta que el artillero solo puede estar en filas menores a 8");
			printf("\nEscribe la fila: ");
			scanf("%d", &artillero_1_jo2[0]);
			printf("\nEscribe la columna: ");
			scanf("%d", &artillero_1_jo2[1]);
			for(int i = artillero_1_jo2[1]; i <= artillero_1_jo2[1]+3; i++){
				campo_2[i][artillero_1_jo2[0]] = 1;
			}
			imprime(campo_2);
			
			//Artillero 2
			printf("\nSegundo artillero: ");
			printf("\nEscribe las coordenadas en donde va a ir el segundo artillero: ");
			printf("\nEscribe la fila: ");
			scanf("%d", &artillero_2_jo2[0]);
			printf("\nEscribe la columna: ");
			scanf("%d", &artillero_2_jo2[1]);
			for(int i = artillero_2_jo2[1]; i <= artillero_2_jo2[1]+3; i++){
				campo_2[i][artillero_2_jo2[0]] = 1;
			}
			imprime(campo_2);
			
			//Bote     
			
			printf("\nBote");
			printf("\nEscribe las coordenadas en donde va a ir el bote ");
			printf("\nEscribe la fila: ");
			scanf("%d", &bote_jo2[0]);
			printf("\nEscribe la columna :");
			scanf("%d", &bote_jo2[1]);
			for(int i = bote_jo2[1]; i <= bote_jo2[1]+1; i++){
				campo_2[i][bote_jo2[0]] = 1;
			}
			imprime(campo_2);
			getch();
			system("cls");
			printf("Tus barcos han sido guardados, la pantalla ha sido borrada, click para continuar");
			getch();
		}
		
		
		//Cambia de jugador 
		contador_jugador++;
	} while (contador_jugador != 2);
	
	// Fin del mudulo de genaración de barcos//
	//------------------------------------------------------------------
	//Ubicar los puntos clave para el jugador 1
	/*Simbología para todos los puntos claves o no
	0 = Hay barco 
	1 = Hay un punto de un barco
	2 = Diste a un barco
	3 = Tienes disparo doble
	4 = Puedes bombardear fila
	5 = Puedes recuperar un barco*/
	 
	//Modulo para tiros dobles

	while(conteo<bonos){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo[phil][columbo]!=1 && campo[phil][columbo]!=2){
			campo[phil][columbo]=3;
			conteo++;
		}
	}

	conteo = 0;
	while(conteo<bonos){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo_2[phil][columbo]!=1 && campo_2[phil][columbo]!=2){
			campo_2[phil][columbo]=3;
			conteo++;
		}
	}

	/*Modulos para bombardear filas*/
	conteo = 0;
	while(conteo<1){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo[phil][columbo]!=1 && campo[phil][columbo]!=2 && campo[phil][columbo]!=3){
			campo[phil][columbo]=4;
			conteo++;
		}
	}

	conteo = 0;
	while(conteo<1){
		phil=rand()%8;
		columbo=rand()%8;
		if (campo_2[phil][columbo]!=1 && campo_2[phil][columbo]!=2 && campo_2[phil][columbo]!=3){
			campo_2[phil][columbo]=4;
			conteo++;
		}
	}

	/* ESTO ES UNA PRUEBA <<BORRAR CUANDO EL CODIGO ESTE LISTO>>*/
	
	imprime(campo);
	imprime(campo_2);
	
	
	
	//LOGISTICA
	//Variables de logistica
	int turnos = 0;
	char recuperar;
	int x_C, y_C, valor_disparo, fila_bombardeada;
	system("cls");
	printf("\nLISTO, ¡QUE EMPIECE EL COMBATE!");
	
	do
	{
		if(turnos == 0){
			printf("\nTurno del jugador 1");
			printf("\nEscribe tu coordenada x :");
			scanf("%d", &x_C);
			fflush(stdin);
			printf("\nEscribe tu coordenada y :");
			scanf("%d", &y_C);
			fflush(stdin);

			valor_disparo = campo_2[x_C][y_C];

			switch (valor_disparo)
			{
			case 0:
			printf("\nFallaste, diste a mar ");
			turnos++;
				break;
			case 1:
			printf("\nHas dado a un barco ");
			campo_2[x_C][y_C] = 2;
			turnos++;
			break;

			case 2:
			printf("\nYa habias dado a un barco");
			turnos++;
			break; 
			
			case 3:
			printf("\nTienes disparo doble :");
			break;

			case 4:
			printf("\nPuedes bombardear una fila :");
			printf("\nEscribe la fila que desea bombardear :");
			scanf("%d", &fila_bombardeada);
			for(int i = 0; i < 10; i++){
				if(campo_2[fila_bombardeada][i] == 1){
					campo[fila_bombardeada][i] = 2;
				}
			}
			turnos++;
			break;

			case 5:
			printf("\nPuedes recuperar un barco :");
			printf("\n a para acorazado \nb para bote \n e para artillero 1 \n j para artillero 2");
			recuperar = getchar();
			switch (recuperar)
			{
			case 'a':
			for(int i = acorazado[1]; i <= acorazado[1]+5; i++){
				campo[acorazado[0]][i] = 1;
			}
				break;

			case 'b':
			for(int i = bote[1]; i <= bote[1]+1; i++){
				campo[i][bote[0]] = 1;
			}
				break;

			case 'e':
			for(int i = artillero_1[1]; i <= artillero_1[1]+3; i++){
				campo[i][artillero_1[0]] = 1;
			}
				break;

			case 'j':
			for(int i = artillero_2[1]; i <= artillero_1[1]+3; i++){
				campo[i][artillero_1[0]] = 1;
			}	
				break;
			
			default:
				break;
			}
			turnos++;
			break;

			default:
			turnos++;
				break;
			}
			printf("\nTu campo se encuentra de esta manera");
			imprime(campo);
			getch();
			system("cls");
			printf("la pantalla ha sido borrada");
			getch();
			printf("\nCampo del rival");
			imprimir_pantalla_espectro(campo_2);
			getch();
			system("cls");
			printf("la pantalla ha sido borrada");
			getch();

			
		}
		else if (turnos == 1)
		{
			printf("\nTurno del jugador 2");
			printf("\nEscribe tu coordenada x :");
			scanf("%d", &x_C);
			fflush(stdin);
			printf("\nEscribe tu coordenada y :");
			scanf("%d", &y_C);
			fflush(stdin);

			valor_disparo = campo[x_C][y_C];

			switch (valor_disparo)
			{
			case 0:
			printf("\nFallaste, diste a mar ");
			turnos--;
				break;
			case 1:
			printf("\nHas dado a un barco ");
			campo[x_C][y_C] = 2;
			turnos--;
			break;

			case 2:
			printf("\nYa habias dado a un barco");
			turnos--;
			break; 
			
			case 3:
			printf("\nTienes disparo doble :");
			break;

			case 4:
			printf("\nPuedes bombardear una fila :");
			printf("\nEscribe la fila que desea bombardear :");
			scanf("%d", &fila_bombardeada);
			for(int i = 0; i < 10; i++){
				if(campo[fila_bombardeada][i] == 1){
					campo[fila_bombardeada][i] = 2;
				}
			}
			turnos--;
			break;

			case 5:
			printf("\nPuedes recuperar un barco :");
			printf("\n a para acorazado \nb para bote \n e para artillero 1 \n j para artillero 2");
			recuperar = getchar();
			switch (recuperar)
			{
			case 'a':
			for(int i = acorazado_jo2[1]; i <= acorazado_jo2[1]+5; i++){
				campo_2[acorazado_jo2[0]][i] = 1;
			}
				break;

			case 'b':
			for(int i = bote_jo2[1]; i <= bote_jo2[1]+1; i++){
				campo_2[i][bote_jo2[0]] = 1;
			}
				break;

			case 'e':
			for(int i = artillero_1_jo2[1]; i <= artillero_1[1]+3; i++){
				campo_2[i][artillero_1_jo2[0]] = 1;
			}
				break;

			case 'j':
			for(int i = artillero_2_jo2[1]; i <= artillero_1_jo2[1]+3; i++){
				campo_2[i][artillero_1_jo2[0]] = 1;
			}	
				break;
			
			default:
				break;
			}
			turnos--;
			break;

			default:
			turnos--;
				break;
			}
			printf("\nTu campo se encuentra de esta manera");
			imprime(campo_2);
			getch();
			system("cls");
			printf("la pantalla ha sido borrada");
			getch();
			printf("\nCampo del rival");
			imprimir_pantalla_espectro(campo);
			getch();
			system("cls");
			printf("la pantalla ha sido borrada");
			getch();
		}
		
		turnos = ganador(campo, campo_2, turnos);
		
		
	} while (turnos != 3);
	
	
	
	
	return 0;
}



void imprimir_pantalla_espectro(int campo[][10]){
	char mar = 178;
	char barco_muerto = 206;
	printf("\n");
	for(int i = 1; i < 10; i++){
		for(int j = 1; j < 10; j++){
			if(campo[i][j] == 2){
				printf("%c", barco_muerto);
				printf(" ");		
			}
			else{
				printf("%c", mar);
				printf(" ");
			}
		}
		printf("\n");
	}
	printf("\n");
}

void imprime(int tablero_partiaccipante[][10]){
	printf("\n");
	for(int i = 1; i < 10; i++){
		for(int j = 1; j < 10; j++){
			printf("%d,", tablero_partiaccipante[i][j]);
		}
		printf("\n");
	}
	printf("\n");   
}

int ganador(int campo[10][10], int campo_2[10][10], int turno){
	int jugador_1 = 0;
	int jugador_2 = 0;
	int i;
	int j;
	
	for(i = 0; i < 10; i++){
		for(j = 0; j < 10; j++){
			if(campo[i][j] == 1){
				jugador_1++;
			}
		}
	}
	for(i = 0; i < 10; i++){
		for(j = 0; j < 10; j++){
			if(campo_2[i][j] == 1){
				jugador_2++;
			}
		}
	}
	
	if(jugador_2 == 0){
		printf("\n ¡FELICIDADES JUGADOR 1, HAZ GANADO EL JUEGO!");
		turno = 3;
	}
	else if (jugador_1 == 0){
		printf("\nA ¡FELICIDADES JUGADOR 2, HAZ GANADO EL JUEGO!");
		turno = 3;
	}
	else{
		turno = turno;
			
		}

	return turno;
}		

