﻿Создание простейшего приложения:
1. Создайте консольное приложение(File->New Project->Visual C#->Windows->Console Application)
2. Добавьте ссылку на библиотеку NLapack.dll(пкм по References->Add Rеference->Browse)
3. Соберите приложение.
4. Зайдите в папку bin/Debug. Добавьте туда файлы blas_win32.*, lapack_win32.*.
5. Скопируйте следующий код в Program.cs и запустите:
using System;
using NLapack;
using NLapack.Matrices;
 
namespace nlapackTestHello
{
    class Program
    {
        static void Main(string[] args)
        {
            var A = new NRealMatrix(3, 3);
            A[0, 0] = 2; A[0, 1] = 5; A[0, 2] = 3;
            A[1, 0] = 1; A[1, 1] = 5; A[1, 2] = 7;
            A[2, 0] = 8; A[2, 1] = 2; A[2, 2] = 3;
 
            var B = new NRealMatrix(3, 3);
 
            //generate upper triangular matrix 
            B.Fill((i, j) => i <= j ? i + j + 1 : 0);
            Console.WriteLine(B);
 
            var lib = new NLapackLib();
 
            var X = new NRealMatrix();
            //solve A * X = B
            lib.SolveSle(A, B, X);
 
            Console.WriteLine(X);
        }
    }
}