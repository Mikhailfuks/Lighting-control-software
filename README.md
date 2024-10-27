using System;
using System.Collections.Generic;

namespace LightingControl
{
    class Program
    {
        static void Main(string[] args)
        {
            LightingSystem lightingSystem = new LightingSystem();
            int choice;

            do
            {
                Console.WriteLine("1. Включить свет");
                Console.WriteLine("2. Выключить свет");
                Console.WriteLine("3. Просмотреть состояние света");
                Console.WriteLine("0. Выход");
                Console.Write("Выберите опцию: ");
                choice = Convert.ToInt32(Console.ReadLine());

                switch (choice)
                {
                    case 1:
                        Console.Write("Введите номер комнаты (1-3): ");
                        int roomOn = Convert.ToInt32(Console.ReadLine());
                        lightingSystem.TurnOnLight(roomOn);
                        break;
                    case 2:
                        Console.Write("Введите номер комнаты (1-3): ");
                        int roomOff = Convert.ToInt32(Console.ReadLine());
                        lightingSystem.TurnOffLight(roomOff);
                        break;
                    case 3:
                        lightingSystem.DisplayLightStatus();
                        break;
                    case 0:
                        Console.WriteLine("Выход из программы.");
                        break;
                    default:
                        Console.WriteLine("Неверный выбор. Попробуйте снова.");
                        break;
                }

            } while (choice != 0);
        }
    }

    public class LightingSystem
    {
        private Dictionary<int, bool> lights; // Словарь для хранения состояния ламп

        public LightingSystem()
        {
            // Инициализация с 3 комнатами, все лампы выключены
            lights = new Dictionary<int, bool>
            {
                { 1, false },
                { 2, false },
                { 3, false }
            };
        }

        public void TurnOnLight(int room)
        {
            if (IsValidRoom(room))
            {
                lights[room] = true;
                Console.WriteLine($"Свет в комнате {room} включен.");
            }
        }

        public void TurnOffLight(int room)
        {
            if (IsValidRoom(room))
            {
                lights[room] = false;
                Console.WriteLine($"Свет в комнате {room} выключен.");
            }
        }

        public void DisplayLightStatus()
        {
            Console.WriteLine("\n--- Состояние света ---");
            for (int i = 1; i <= lights.Count; i++)
            {
                Console.WriteLine($"Комната {i}: {(lights[i] ? "Включен" : "Выключен")}");
            }
            Console.WriteLine("-----------------------\n");
        }

        private bool IsValidRoom(int room)
        {
            if (room < 1 || room > lights.Count)
            {
                Console.WriteLine("Неверный номер комнаты. Пожалуйста, введите номер от 1 до 3.");
                return false;
            }
            return true;
        }
    }
}
