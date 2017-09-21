# Motif
Motif and ADN
package Bio_1; //Paquete donde esta el createfile y el letor de ADN

/**
 * @author Danilo Castilla
 * @version 1.0
 * @date 12/Sept/2017
 */

import java.io.*; //Importar la libreria para obtener el Buffered
import java.util.*; //Importar la libreria para obtener el Random

public class Createfile { //Clase donde crearemos el archivo de tipo "umd"
	
	
	public Createfile() throws IOException{ //Metodo de lineas del archivo
	
	BufferedWriter bw = new BufferedWriter ( new FileWriter ( "Sequence.umd" ) );
	for(int i = 0; i<1000; i++)
	{
		
		bw.write(createExperimentalRead()); //Llamamos al metodo Experimental read que es el que asigna los valores
		
	}
	
	bw.flush();
	
	}//Fin metodo CreateFile
	
	public String createExperimentalRead() //Asignar letras, nuemros y espacion 
	{
		//Declaracion de variable
		String read = " ";
		Random rd = new Random();
		int number1 = Math.abs(rd.nextInt()); //Generar un numero aleatoria y sacarle su valor absoluto, para que siempre de positivo
		int lenght = 5 + rd.nextInt(26); //Generar una longitud aleatoria entre los numeros 5 y 25 (El 26 no lo toma)
		
		read = number1 + "," +  (number1 + lenght) + "," + createSequences(lenght) + "\n"; //Concatenar los resultados finalizando con un "Enter"
		
		return read; //Retornar la linea hecha entre nuemros y letras
		
		
	} //Fin metodo ExperimentalRead
	

	public String createSequences(int lenght) 
	{//Metodo Crear secuencia
		
		String sequence = " ";
		Random rd = new Random(); //Crear objeto instancial a Random
		
		for(int i = 0 ; i<lenght; i++)
		{
			
			switch(rd.nextInt(4)){ //Generar numeros aleatorios enre 0 y 3
			
			case 0:
			{
				sequence += "A";
			}
			break;
			
			case 1:
			{
				sequence += "C";
			}
			break;
			
			case 2:
			{
				sequence += "G";
			}
			break;
			
			case 3:
			{
				sequence += "T";
			}
			break;
			
			}
			
		}
		return sequence; //Retornar las letras escogidas
		
	}//Fin metodo Secuancia
	
	public static void main(String args[]) throws IOException //Metodo Main
	{
		
		Createfile cf = new Createfile(); //Cuando inicia el programa, lo va a dirigir al metodo CreateFile
		
	}//Fin metodo Main
	
} //Fin de la Clase

//Se finaliza la clase principal del paquete y se crea una nueva en el mismo

package Bio_1; //Paquete donde esta el createfile y el letor de ADN

/**
 * @author Danilo Castilla
 * @version 1.0
 * @date 12/Sept/2017
 */

import java.io.*; //Importar la libreria para obtener el Buffered
import java.util.*; //Importar la libreria para obtener el Random

public class Reader_ADN { //Clase en el que vamos a comparar un dato por consola, por una de la cadena original

	
	public static int numberReads(String motif) throws IOException{ //Metodo Numero de veces que se repite una cadena con un parametro String
		
		BufferedReader br = new BufferedReader ( new FileReader ( "Sequence.umd" )); //Se lee el archivo creado anteriormente
		//Declarar e inicializar variables
		int lines=0, linesMotif=0; //Son enteros porque van a devolver un nunero entero
		String read = br.readLine(); //Leer la primera linea del archivo
		while(read!=null) //Se hace para cuando detecte un espacio, salga del ciclo While, ya que nos abemos cuantas lineas tiene el archivo que se leera
		{
			
			if(read.split(",")[2].contains(motif)) //Como son 3 cadenas creadas, dos de nuemros y una de letras, se separan con un Split que recibe como parametro una coma ","
			{                                      //Para que los separe por medio de un arreglo, y se toma e segundo que son las letras
				linesMotif += 1;  //usamos el contains para saber si la cadena que escribimos esta en la cadena principal de ser asi, aunmenta el contador de uno en uno
			}
			
			lines += 1; //De no ser asi, aumenta el numero de lienas para pasar a la siguiente
			read = br.readLine(); //Aquie es donde se repite el procedimiento
			
		} //Fin del ciclo While
		
		return linesMotif; //Retornar el numero de veces que se encuantra la cadena por consola en la original
		
	}
	
	public static void main(String[] args) throws IOException { //Metodo Main
		
		BufferedReader br = new BufferedReader (new InputStreamReader(System.in));
		String A = br.readLine(); //Se leera la cadena escrita por consola
		int R = Reader_ADN.numberReads(A); //Llama a metodo Leer ADN y entra como parametro lo escrito por consola, lo cual es un String
		System.out.println(R); //Mostrar por pantalla las veces que se repite la cadena
		
	}//Fin del metodo Main
	
}//Fin de la Clase
