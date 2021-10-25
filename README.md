Código completo del juego del Laberinto hecho en la consola de comando de windows. Lenguaje utilizado: C#




using System;

namespace Laberinto
{
    class Program
    {
        //AL CAMBIAR LA ALTURA Y EL ANCHO HAY QUE REPOSICIONAR LAS POSICIÓN DEL JUGADOR (X,Y) Y LA POSICIÓN DEL CURSOR (X1,Y2)
        
        const int Altura = 30; //Altura del trablero del juego
        const int Ancho = 30; //Anchura del trablero del juego

        public static int [] grid = new int[Altura * Ancho];        
        static int X = 20; //Posición del jugador en el eje X
        static int Y = 29; //Posición del jugador en el eje Y
        static int X1 = 18; //Posición del cursor en el eje X
        static int Y2 = 30; //Posición del cursor en el eje Y
        static int Monedas = 20; //Número de las monedas para el juego
        static int X_Moneda = 1; //Posición del cursor en el eje X para escribir el texto durante el juego
        static int Y_Moneda = 1; //Posición del cursor en el eje Y para escribir el texto durante el juego
        static bool Jugar = true; //Bucle para mantener el juego activo
        static bool Juego = true; //Bucle para mantener TODO el juego activo
        static bool Instrucciones = true; //Bucle para el menú principal
        static bool Pepe = true; //Mini bucle para que se pinte el jugador después de cada partida


        static void Main(string[] args)
        {
            
            while (Juego == true)
            {
                Menu1();

                while (Instrucciones == true)
                {


                    Console.Write("\n Dime que quieres hacer:\n");
                    Console.Write("\n F1. Jugar\n F2. Controles del juego\n F3. Salir");
                    Menu2();
                    
                }
                Reset();
                

                while (Pepe == true)
                {

                    grid[X + Ancho * Y] = 64;
                    Pepe = false;


                }

                Pintar();
                

               
                Console.SetCursorPosition(X1, Y2);


                while (Jugar == true)
                {


                    Jugador();
                }
                
                Console.Clear();
            }
            
                             
            

        } //Lo que hace que funcione todo


        static void Reset()
        {

            
            Random aire = new Random();

            int a;
            int X_Tesoro = aire.Next(Ancho - X + 5); //Posición aleatoria en el eje X para el premio
            int Y_Tesoro = aire.Next(Altura - Y + 5); //Posición aleatoria en el eje Y para el premio

            for (int i = 0; i < Altura * Ancho; i++) //El tablero se hace en función de la Altura y el Ancho
            {

                a = aire.Next(2); //La consola saca un valor aleatorio entre 0 o 1 y asi se crea el tablero

                if(a == 0)
                {

                    grid[i] = 00; //00 = hueco vacio


                }else if(a == 1)
                {


                    grid[i] = 216; //216 = muro

                }


                grid[X_Tesoro + Ancho * Y_Tesoro] = 35;  //Posición del premio. 
                
                               


            }

            Pepe = true;
            X = 20;
            Y = 29;
            X1 = 18;
            Y2 = 30;
            Monedas = 20;

        } //Si queremos cambiar las dimensiones del juego, hay que reposicionar al jugador
        static void Pintar()
        {

            for (int i = 0; i< Altura * Ancho; i++)
            {

                char letra = Convert.ToChar(grid[i]);
                Console.Write(letra);

                
                if (i % Ancho  == 1) //Se hace un salto de línea
                {
                    Console.Write("\n");

                }

                
                



            }





        } //El tablero se pinta en función de la Altura y el Ancho
        static void Menu1()
        {
            Console.Write(" \n Bienvenido:\n");



        } //Pequeño mensaje que sale solamente al incio o cada vez que vuelves al menú


        static void Menu2()
        {

            
            ConsoleKey key1 = Console.ReadKey(true).Key;

            Console.Clear();


            if (key1 == ConsoleKey.F1)
            {


                Console.Clear();


                Instrucciones = false;
                Jugar = true;
                Juego = true;



                Reset();



            } //Activa el juego
            
            if (key1 == ConsoleKey.F2)
            {

                Console.Clear();
                Console.Write("\n INSTRUCCIONES: \n\n Debes de tratar de llegar al premio (#) moviendote por el tablero\n Tú eres un (@) y tienes la posibilidad de usar unas armas para poder abrite paso\n" +
                    "\n Las teclas A, W y D sirven para moverte: \n\n A: Movimiento hacia la izquierda \n W: Movimiento hacia arriba \n D: Movimiento hacia la derecha \n\n"
                    + " Las teclas I, O y P sirven para usar tus armas: \n\n I: Elimina 'X' bloques de manera aleatoria [Tranquilo que no se puede borrar tu premio :)]\n " +
                    "O: Elimina 3 bloques hacia arriba \n P: Elimina 3 bloques. 1 hacia arriba y 1 hacia cada diagonal de tu posición\n\n" + " **Si te quedas sin monedas o llegas a la última fila, perderás y vovlerás al menú de inicio**\n\n");
                
                

            } //Muestra las instrucciones

            if (key1 == ConsoleKey.F3)
            {
                Console.Clear();
                Instrucciones = false;
                Juego = false;
                Jugar = false;

            } //Cierra el juego
                                 


        } //Menú principal

        static void Menu3()
        {


            Console.Clear();
            Instrucciones = true;
            //Jugar = true;
            Juego = true;
            Console.Write("\n\n\n\t\t\t ¡¡¡HAS PERDIDO!!! :(");
            Console.WriteLine("\t\t\tPulsa cualquier tecla para volver al menú");
            ConsoleKey key1 = Console.ReadKey(true).Key;
            if (key1 == ConsoleKey.Enter) //Está puesto 'Enter' pero solamente para que después de tocar cualquier tecla se active
            {

                


            }

            Jugar = false;


        } //Derrota


        static void Ganar()
        {
            Console.Clear();
            Instrucciones = true;
            //Jugar = true;
            Juego = true;
            Console.Write("\n\n\n\t\t\t ¡¡¡HAS GANADO :) !!!");
            Console.WriteLine("\t\t\tPulsa cualquier tecla para vovler para volver al menú");
            ConsoleKey key2 = Console.ReadKey(true).Key;
            if(key2 == ConsoleKey.Enter) //Está puesto 'Enter' pero solamente para que después de tocar cualquier tecla se active
            {

                


            }


        } //Victoria
                
        public static void Jugador()
        {




            if (Monedas >= 0 && Y >= 1)
            {

                Console.SetCursorPosition(X_Moneda, Y_Moneda); //Pone la posición para el inicio del texto durante el juego
                Console.Write("\t\t\t\t\t Monedas = " + Monedas);
                Console.WriteLine("\n\t\t\t\t\t Arma 1 (O) '3 $' = Elimina 3 bloques hacia arriba.");
                Console.Write("\t\t\t\t\t Arma 2 (I) '5 $' = Elimina 'X' bloques hacia arriba de manera aleatoria.");
                Console.WriteLine("\n\t\t\t\t\t Arma 3 (P) '1 $' = Elimina 1 bloque hacia arriba y 1 hacia cada diagonal de tu posición.");
                Console.Write("\t\t\t\t\t Pulsa 'R' para salir del juego.");



                if (Monedas <= 10)
                {


                    Console.WriteLine("\n\t\t\t\t\t\t\t ¡¡¡Cuidado, te quedan pocas monedas!!!");

                } //Pequeño mensaje recordatorio durante el juego

                if (Monedas == 0)
                {


                    Console.WriteLine("\n\n\t\t\t\t\t\t\t ¡¡¡Cuidado, no te quedan más monedas!!!");

                } //Pequeño mensaje recordatorio durante el juego


                grid[X + Ancho * Y] = 64;
                Console.SetCursorPosition(X1, Y2);


                ConsoleKey key = Console.ReadKey(true).Key;

                if(key == ConsoleKey.R)
                {
                    Jugar = false;
                    Instrucciones = true;
                    Juego = true;


                    //REINICIAR JUEGO

                } //Si se pulsa 'R', te lleva al menú principal

                if (key == ConsoleKey.D)
                {
                    if (X <= Ancho)
                    {

                        if (grid[(X + 1) + Ancho * Y] == 00)
                        {

                            grid[X + Ancho * Y] = 00;
                            X += 1;
                            grid[X + Ancho * Y] = 64;
                            X1 += 1;
                            Console.Clear();
                            Pintar();
                            Console.SetCursorPosition(X1, Y2);

                        }
                        else if (grid[(X + 1) + Ancho * Y] == 216)
                        {

                            grid[X + Ancho * Y] = 00;
                            grid[X + Ancho * Y] = 64;
                            Console.Clear();
                            Pintar();
                            Console.SetCursorPosition(X1, Y2);

                        }




                    } //Movimiento

                    if (grid[(X + 1) + Ancho * Y] == 35)
                    {
                        Jugar = false;

                        Ganar();


                    } //Victoria




                } //Si se pulsa 'D', te mueves hacia la derecha
                else if (key == ConsoleKey.A)
                {

                    if (X > 2)
                    {

                        if (grid[(X - 1) + Ancho * Y] == 00)
                        {
                            grid[X + Ancho * Y] = 00;
                            X -= 1;
                            grid[X + Ancho * Y] = 64;
                            X1 -= 1;
                            Console.Clear();

                            Pintar();
                            Console.SetCursorPosition(X1, Y2);



                        }
                        else if (grid[(X - 1) + Ancho * Y] == 216)
                        {
                            grid[X + Ancho * Y] = 00;
                            grid[X + Ancho * Y] = 64;
                            Console.Clear();

                            Pintar();
                            Console.SetCursorPosition(X1, Y2);


                        }




                    } //Movimiento

                    if (grid[(X - 1) + Ancho * Y] == 35)
                    {
                        Jugar = false;
                        Ganar();


                    } //Victoria


                } //Si se pulsa 'A', te mueves hacia la izquierda
                else if (key == ConsoleKey.W)
                {

                    if (Y > 0)
                    {

                        if (grid[X + Ancho * (Y - 1)] == 00)
                        {
                            grid[X + Ancho * Y] = 00;
                            Y -= 1;
                            grid[X + Ancho * Y] = 64;
                            Y2 -= 1;
                            Console.Clear();

                            Pintar();
                            Console.SetCursorPosition(X1, Y2);



                        }
                        else if (grid[X + Ancho * (Y - 1)] == 216)
                        {
                            grid[X + Ancho * Y] = 00;
                            grid[X + Ancho * Y] = 64;
                            Console.Clear();

                            Pintar();
                            Console.SetCursorPosition(X1, Y2);



                        }

                        if (Y > 0)
                        {
                            if (grid[X + Ancho * (Y - 1)] == 35)
                            {
                                Jugar = false;
                                Ganar();


                            }


                        } //Victoria



                    } //Movimiento y victoria



                } //Si se pulsa 'W', te mueves hacia arriba

                
                if (Monedas >= 0)
                {

                    if (key == ConsoleKey.O)
                    {

                        


                        if ((Y - 3) > -1 && (Y - 2) >= -1)
                        {



                            if (grid[X + Ancho * (Y - 1)] != 35 && grid[X + Ancho * (Y - 2)] != 35 && grid[X + Ancho * (Y - 3)] != 35)
                            {
                                Monedas -= 3; //Al usarse, quita 3 monedas

                                grid[X + Ancho * (Y - 1)] = 00;
                                grid[X + Ancho * (Y - 2)] = 00;
                                grid[X + Ancho * (Y - 3)] = 00;
                                Console.Clear();

                                Pintar();
                                Console.SetCursorPosition(X1, Y2);


                            }
                            else if (grid[X + Ancho * (Y - 1)] != 35 && grid[X + Ancho * (Y - 2)] != 35 && grid[X + Ancho * (Y - 3)] == 35)
                            {


                                grid[X + Ancho * (Y - 1)] = 00;
                                grid[X + Ancho * (Y - 2)] = 00;

                                Console.Clear();

                                Pintar();
                                Console.SetCursorPosition(X1, Y2);

                            }






                        }







                    }



                } //Arma 1. (O) Quita 3 casillas hacia arriba.

                if (Monedas >= 0)
                {

                    if (key == ConsoleKey.I)
                    {


                        Monedas -= 5; //Al usarse, quita 5 monedas

                        Random armas = new Random();

                        int Arma;
                        int X_Arma;
                        int Y_Arma;

                        for (int i = 0; i < 70; i++)
                        {
                            X_Arma = armas.Next(Ancho);
                            Y_Arma = armas.Next(Altura);

                            Arma = armas.Next(3);

                            if (Arma == 0)
                            {
                                if ((grid[X_Arma + Ancho * Y_Arma] != 35) && (grid[X_Arma + Ancho * Y_Arma] != 64))
                                {

                                    grid[X_Arma + Ancho * Y_Arma] = 00;


                                }

                                if (grid[X_Arma + Ancho * Y_Arma] == 35)
                                {

                                    grid[X_Arma + Ancho * Y_Arma] = 35;


                                }

                                if (grid[X_Arma + Ancho * Y_Arma] == 64)
                                {

                                    grid[X_Arma + Ancho * Y_Arma] = 64;


                                }


                            }
                            else if (Arma == 1)
                            {
                                if ((grid[X_Arma + Ancho * Y_Arma] != 35) && (grid[X_Arma + Ancho * Y_Arma] != 64))
                                {

                                    grid[X_Arma + Ancho * Y_Arma] = 00;


                                }

                                if (grid[X_Arma + Ancho * Y_Arma] == 35)
                                {

                                    grid[X_Arma + Ancho * Y_Arma] = 35;


                                }

                                if (grid[X_Arma + Ancho * Y_Arma] == 64)
                                {

                                    grid[X_Arma + Ancho * Y_Arma] = 64;


                                }

                            }


                            // pinta posicion jugador // grid[X + Ancho * Y] = 00;




                        } //Este arma se basa en la suerte, según la máquina decida, te borra una cantidad aleatoria de muros


                        Console.Clear();

                        Pintar();
                        Console.SetCursorPosition(X1, Y2);

                    }



                } //Arma 2. (I) Quita 'X' casillas hacia arriba de manera aleatoria.

                if (Monedas >= 0 && grid[X + Ancho * Y] != 35)
                {

                    if (key == ConsoleKey.P)
                    {




                        if (grid[X + Ancho * (Y - 1)] != 35 && grid[(X - 1) + Ancho * (Y - 1)] != 35 && grid[(X + 1) + Ancho * (Y - 1)] != 35)
                        {

                            Monedas -= 1; //Al usarse, quita 1 monedas

                            grid[X + Ancho * (Y - 1)] = 00;
                            grid[(X - 1) + Ancho * (Y - 1)] = 00;
                            grid[(X + 1) + Ancho * (Y - 1)] = 00;
                            Console.Clear();

                            Pintar();
                            Console.SetCursorPosition(X1, Y2);


                        }



                    }



                } //Arma 3. (P) Quita 1 casillas hacia arriba y 1 hacia cada diagonal.

                
            } //Movimiento del jugador y las armas

            if(Monedas < 0 || Y < 1)
            {

                Menu3();
                

            } //Métodos de derrota, quedarse por debajo de '0' monedas o estar en la posición más alta del tablero

        } //Todo sobre el movimiento y las armas
                              
        
    }
}
