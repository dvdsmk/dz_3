import random


class House:
    def __init__(self):
        self.mess = 0
        self.food = 0


class Auto:
    car_list = {
        'BMW': {'fuel': 100, 'durability': 100, 'consumption': 6},
        'ZAZ': {'fuel': 50, 'durability': 40, 'consumption': 10},
        'Volvo': {'fuel': 70, 'durability': 150, 'consumption': 8},
        'Ferrari': {'fuel': 80, 'durability': 120, 'consumption': 14},
    }

    def __init__(self):
        self.brand = random.choice(list(Auto.car_list))
        self.fuel = Auto.car_list[self.brand]['fuel']
        self.durability = Auto.car_list[self.brand]['durability']
        self.consumption = Auto.car_list[self.brand]['consumption']

    def drive(self):
        if self.durability > 0 and self.fuel >= self.consumption:
            print('Driving...')
            self.fuel -= self.consumption
            self.durability -= 1
            return True
        else:
            print('This car can\'t go!')
            return False


class Job:
    job_list = {
        'Python developer': {'salary': 40, 'sadness': 3},
        'Java developer': {'salary': 50, 'sadness': 10},
        'C++ developer': {'salary': 45, 'sadness': 25},
        'Rust developer': {'salary': 70, 'sadness': 1},
    }

    def __init__(self):
        self.job_title = random.choice(list(Job.job_list))
        self.salary = Job.job_list[self.job_title]['salary']
        self.sadness = Job.job_list[self.job_title]['sadness']


class Girlfriend:
    def __init__(self):
        self.happiness = 0

    def positive_event(self):
        self.happiness += 1

    def negative_event(self):
        self.happiness -= 1


class Human:
    def __init__(
            self,
            name='Human',
            job=None,
            home=None,
            car=None,
            girlfriend=None
    ):
        self.name = name
        self.money = 100
        self.happiness = 50
        self.satiety = 50
        self.job = job
        self.car = car
        self.home = home
        self.girlfriend = girlfriend

    def get_home(self):
        self.home = House()

    def get_car(self):
        self.car = Auto()

    def get_job(self):
        if self.car.drive():
            self.job = Job()
        else:
            self.to_repair()

    def to_repair(self):
        self.car.durability += 100
        self.money -= 50

    def eat(self):
        if self.home.food <= 0:
            self.shopping('food')
        else:
            if self.satiety >= 100:
                self.satiety = 100
            else:
                self.satiety += 5
                self.home.food -= 5

    def shopping(self, goal):
        if self.car.drive():
            pass
        else:
            if self.car.fuel < self.car.consumption:
                goal = 'fuel'
            else:
                self.to_repair()
                return
        if goal== 'fuel':
            print('I bought fuel')
            self.money -= 100
            self.car.fuel += 100
        elif goal == 'food':
            print('I bought food')
            self.money -= 50
            self.home.food += 50
        elif goal == 'sweets':
            print('I bought sweets!!!')
            self.money -= 15
            self.satiety += 2
            self.happiness += 10

        def work(self):
            if self.car.drive():
                pass
            else:
                if self.car.fuel < self.car.consumption:
                    self.shopping('fuel')
                    return
                else:
                    self.to_repair()
                    return
            self.money += self.job.salary
            self.happiness -= self.job.sadness
            self.satiety -= 4

        def chill(self):
            self.happiness += 10
            self.home.mess += 5

        def clean_home(self):
            self.happiness -= 5
            self.home.mess = 0

        def status(self, day):
            day_str = f'Today the {day} day of {self.name}\'s life'
            print(f'{day_str:=^50}')
            print('\n')
            human_info = f'{self.name}\'s info'
            print(f'{human_info:^50}')
            print('\n')
            print(f'money: {self.money}')
            print(f'satiety: {self.satiety}')
            print(f'happiness: {self.happiness}')
            home_info = 'Home info'
            print(f'{home_info:^50}')
            print('\n')
            print(f'mess: {self.home.mess}')
            print(f'food: {self.home.food}')
            car_info = f'{self.car.brand} car info'
            print(f'{car_info:^50}')
            print('\n')
            print(f'fuel: {self.car.fuel}')
            print(f'durability: {self.car.durability}')

        def is_alive(self):
            if self.happiness < 0:
                print('Depression...')
                return False
            elif self.satiety < 0:
                print('Dead...')
                return False
            elif self.money < -500:
                print('Bankrupt')
                return False
            else:
                return True

        def live_a_day(self, day):
            if not self.is_alive():
                return False
            if self.home is None:
                print('Settled in the house')
                self.get_home()
            if self.car is None:
                self.get_car()
                print(f'I bought a car {self.car.brand}')
            if self.job is None:
                self.get_job()
                print(f'I got a job {self.job.job_title} with salary {self.job.salary}')
            self.status(day)
            dice = random.randint(1, 4)
            if self.satiety < 20:
                print('Ill go to eat')
                self.eat()
            elif self.happiness < 20:
                if self.home.mess <= 15:
                    print('Lets chill')
                    self.chill()
                else:
                    print('I need to clean')
                    self.clean_home()
            elif self.money < 0:
                print('Start working')
                self.work()
            elif self.car.durability < 15:
                print('I need to repair my car')
                self.to_repair()
            elif dice == 1:
                print('Lets chill')
                self.chill()
            elif dice == 2:
                print('Start working')
                self.work()
            elif dice == 3:
                print('I need to clean')
                self.clean_home()
            elif dice == 4:
                print('Time for sweets!')
                self.shopping('sweets')
            return True

        nick = Human('Nick')
        for day in range(1, 8):
            if not nick.live_a_day(day):
                break

