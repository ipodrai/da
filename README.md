СТРУКТУРА ПРОЕКТА


1.
   Структура Monitor

struct Monitor {
    std::string manufacturer; // Фирма-производитель
    int screenSize;           // Размер экрана (в дюймах)
    double price;             // Цена

    void printInfo() const {
        std::cout << "Manufacturer: " << manufacturer << "\n"
                  << "Screen Size: " << screenSize << " inches\n"                     
                  << "Price: $" << price << "\n"
                  << "--------------------------\n";
    }
};


Содержит три поля: производитель, размер экрана и цена.
Метод printInfo выводит информацию о мониторе в консоль.




2.
   Функция inputMonitor

void inputMonitor(Monitor* monitor) {
    std::cout << "Enter manufacturer: ";
    std::cin >> monitor->manufacturer;
    std::cout << "Enter screen size (in inches): ";
    std::cin >> monitor->screenSize;
    std::cout << "Enter price ($): ";
    std::cin >> monitor->price;
}


Функция заполняет данные монитора через консоль.



3.
   Функция createMonitor

void createMonitor(std::vector<Monitor*>& monitors) {
    Monitor* monitor = new Monitor();
    inputMonitor(monitor);
    monitors.push_back(monitor);
    std::cout << "Monitor added successfully!\n";
}


Функция создает новый экземпляр монитора, заполняет его данными и добавляет в вектор.


4.
   Функция printAllMonitors

void printAllMonitors(const std::vector<Monitor*>& monitors) {
    if (monitors.empty()) {
        std::cout << "No monitors available.\n";
        return;
    }
    for (const auto& monitor : monitors) {
        monitor->printInfo();
    }
}


Функция выводит информацию о всех мониторах, хранящихся в векторе.


5.
   Функция deleteMonitor

void deleteMonitor(std::vector<Monitor*>& monitors) {
    if (monitors.empty()) {
        std::cout << "No monitors to delete.\n";
        return;
    }
    std::cout << "Enter the index of the monitor to delete (0-" << monitors.size() - 1 << "): ";
    int index;
    std::cin >> index;
    if (index >= 0 && index < monitors.size()) {
        delete monitors[index];
        monitors.erase(monitors.begin() + index);
        std::cout << "Monitor deleted successfully!\n";
    } else {
        std::cout << "Invalid index.\n";
    }
}


Функция удаляет монитор из вектора по индексу и освобождает выделенную память.


6.

  Главная функция main
int main() {
    std::vector<Monitor*> monitors;

    while (true) {
        std::cout << "\nMenu:\n"
                  << "1. Add a monitor\n"
                  << "2. Print all monitors\n"
                  << "3. Delete a monitor\n"
                  << "4. Exit\n"
                  << "Enter your choice: ";
        int choice;
        std::cin >> choice;

        switch (choice) {
            case 1:
                createMonitor(monitors);
                break;
            case 2:
                printAllMonitors(monitors);
                break;
            case 3:
                deleteMonitor(monitors);
                break;
            case 4:
                for (auto& monitor : monitors) {
                    delete monitor;
                }
                monitors.clear();
                std::cout << "Exiting program. Goodbye!\n";
                return 0;
            default:
                std::cout << "Invalid choice. Try again.\n";
        }
    }

    return 0;
}

Главная функция реализует меню, позволяющее пользователю взаимодействовать с программой





Пример работы программы:
Запуск программы

Menu:
1. Add a monitor
2. Print all monitors
3. Delete a monitor
4. Exit
Enter your choice: 1
Enter manufacturer: Dell
Enter screen size (in inches): 24
Enter price ($): 199.99
Monitor added successfully!

Просмотр списка мониторов

Menu:
1. Add a monitor
2. Print all monitors
3. Delete a monitor
4. Exit
Enter your choice: 2
Manufacturer: Dell
Screen Size: 24 inches
Price: $199.99
--------------------------

Удаление монитора

Menu:
1. Add a monitor
2. Print all monitors
3. Delete a monitor
4. Exit
Enter your choice: 3
Enter the index of the monitor to delete (0-0): 0
Monitor deleted successfully!

Выход из программы

Menu:
1. Add a monitor
2. Print all monitors
3. Delete a monitor
4. Exit
Enter your choice: 4
Exiting program. Goodbye!
