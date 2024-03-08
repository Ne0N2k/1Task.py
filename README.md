# Задача 1. Тарасов Николай
from typing import List, Dict #импортируем типы данных List и Dict из модуля typing, чтобы могли использовать их в определении типов.

class DataIter:
    def __init__(self, input_data: List[dict], type_limitations: Dict[int, int]):
        self.data = input_data #сохраняем входные данные в атрибут self.data.
        self.limitations = type_limitations #сохраняем ограничения типов в атрибут self.limitations.
        self.usage_counter = {type_id: 0 for type_id in type_limitations} #инициализируем счетчик использования для каждого типа входных данных
        self.index = 0 #Устанавливаем начальное значение индекса для итерации данных.

    def __iter__(self):
        return self #возвращаем сам объект итератора.

    def __next__(self):
        while self.index < len(self.data):#начинаем цикл while, который будет выполняться, пока значение self.index меньше длины списка входных данных self.data.
            current_item = self.data[self.index] #получаем текущий элемент из списка входных данных, используя значение self.index в качестве индекса.
            self.index += 1 #получаем текущий элемент из списка входных данных, используя значение self.index в качестве индекса.
            item_type = current_item["type"] # извлекаем тип текущего элемента и сохраняем его в переменной item_type
            if self.usage_counter[item_type] < self.limitations[item_type]:#проверяем, не превышает ли использование текущего типа ограничение, заданное в self.limitations
                self.usage_counter[item_type] += 1 #Если ограничение не превышено,увеличиваем счетчик использования для текущего типа.
                return current_item #Если ограничение не превышено, мы возвращаем текущий элемент.
        raise StopIteration #Если ограничение превышено для текущего типа, вызываем исключение StopIteration, чтобы указать, что итерация по данным должна быть прекращена.

if __name__ == "__main__":
    data = [{"type": 1, "data": "some_string"}, {"type": 2, "data": "some_string"}]
    limitations = {1: 1, 2: 0}
    iter_instance = DataIter(data, limitations) 
    for item in iter_instance:
        print(f"{item['type']} - {item['data']}")
