import random
import math

# Функция генерации соседнего решения
def get_neighbor(x, step_size=0.1):
    neighbor = x[:]
    index = random.randint(0, len(x) - 1)
    neighbor[index] += random.uniform(-step_size, step_size)
    return neighbor

# Основной алгоритм имитации отжига
def simulated_annealing(objective, bounds, n_iterations, step_size, temp):
    # Инициализация начального решения
    best = [random.uniform(bound[0], bound[1]) for bound in bounds]
    best_eval = objective(best)
    current, current_eval = best, best_eval
    scores = [best_eval]
    
    for i in range(n_iterations):
        # Уменьшение температуры
        t = temp / float(i + 1)
        
        # Генерация нового решения
        candidate = get_neighbor(current, step_size)
        candidate_eval = objective(candidate)
        
        # Проверка на принятие нового решения
        if candidate_eval > best_eval or random.random() < math.exp((candidate_eval - current_eval) / t):
            current, current_eval = candidate, candidate_eval
            
        if candidate_eval > best_eval:
            best, best_eval = candidate, candidate_eval
            
        scores.append(best_eval)
        
        # Вывод прогресса
        if i % 100 == 0:
            print(f"Итерация {i}, Температура {t:.3f}, Лучшая оценка {best_eval:.5f}")
            
    return best, best_eval, scores

# Пример использования
# Целевая функция (например, функция Растригина)
def objective_function(x):
    return sum([(xi**2 - 10*math.cos(2*math.pi*xi) + 10) for xi in x])

# Определение границ поиска
bounds = [(-5.0, 5.0) for _ in range(2)]  # для двумерной функции
n_iterations = 1000
step_size = 0.1
temp = 10

# Запуск алгоритма
best, score, scores = simulated_annealing(objective_function, bounds, n_iterations, step_size, temp)
print(f'Лучшее решение: {best}')
print(f'Лучшая оценка: {score}')
