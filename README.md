// lab1_zagrebaev.cpp : Этот файл содержит функцию "main". Здесь начинается и заканчивается выполнение программы.
//

//#include <iostream>
using namespace std;

class Character {
protected:
    int damage;
    int coordinate;    
    int range;

    virtual void atack();
    void stepRight() {
        this->coordinate -= 1;
    };
    void stepLeft() {
        this->coordinate += 1;
    };
public:
    int health = 100;
    void getDamage(int dam) {
        health -= dam;
    }

    int giveCoord() {
        return coordinate;
    }
    
    void chooseAction(int dis, Character* me, Character* enemy) {
        if (dis > range)
            if (dis > 0) stepRight;
            else stepLeft;
        else if (me->health < enemy->health) {
            if (dis > 0) stepRight;
            else stepLeft;
        }
        else atack();
    }

};


class Archer : public Character {
private:
    void atack(Character ch) {
        ch.getDamage(damage);
    }

public: 
    Archer(int dam, int ran) {
    damage = dam;
    range = ran;
    coordinate = 0;
}
    
        
};

class Paladin : public Character {
private:
    void atack(Character* ch) {
        ch->getDamage(damage);
        health += 1;
    }
    void heal() {
        health += 10;
    }

public:
    Paladin(int dam, int ran) {
        damage = dam;
        range = ran;
        coordinate = 9;
    }
    void chooseAction(int dis, Character* me, Character* enemy) {
        if (dis > range)
            if (dis > 0) stepRight;
            else stepLeft;
        else if (me->health < enemy->health) {
            heal();
        }
        else atack(enemy);
    }
};

int main()
{
    Character* arch = new Archer(5, 3);
    Character* pal = new Paladin(6, 1);
    int dis = 0;
    while (arch->health != 0 && pal->health != 0) {
        
        dis = pal->giveCoord() - arch->giveCoord();
        arch->chooseAction(dis, arch, pal);
        dis = arch->giveCoord() - pal->giveCoord();
        pal->chooseAction(dis, pal, arch);
    }
    //cout << "Hello World!\n";
}

// Запуск программы: CTRL+F5 или меню "Отладка" > "Запуск без отладки"
// Отладка программы: F5 или меню "Отладка" > "Запустить отладку"

// Советы по началу работы 
//   1. В окне обозревателя решений можно добавлять файлы и управлять ими.
//   2. В окне Team Explorer можно подключиться к системе управления версиями.
//   3. В окне "Выходные данные" можно просматривать выходные данные сборки и другие сообщения.
//   4. В окне "Список ошибок" можно просматривать ошибки.
//   5. Последовательно выберите пункты меню "Проект" > "Добавить новый элемент", чтобы создать файлы кода, или "Проект" > "Добавить существующий элемент", чтобы добавить в проект существующие файлы кода.
//   6. Чтобы снова открыть этот проект позже, выберите пункты меню "Файл" > "Открыть" > "Проект" и выберите SLN-файл.
