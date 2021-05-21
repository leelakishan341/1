
import random
import copy
import math
#import numpy as np
import matplotlib as plt

#initialization
POPULATION_SIZE=20
CITIES_SIZE=20
TOUR_SIZE=21
NUM_EXECUTION=9999
population=[]
x=[]
y=[]

tour= [[0 for x in range(TOUR_SIZE)] for y in range(TOUR_SIZE)]
dcidade=[[0 for x in range(POPULATION_SIZE)] for y in range(POPULATION_SIZE)]
distance=[0 for x in range(POPULATION_SIZE)]
parentsone=None
parentstwo=None
costByExecution=[]

"""Generate the first population"""
def generateFirstPopulation():
   #for each position, generates a new possible path
    for _ in range(1,POPULATION_SIZE +1):
        generatePossiblePath()
"""Generate a new possible path for a population """
def generatePossiblePath():
    path=[]
    for _ in range(1,CITIES_SIZE + 1):
        randomNum = random.randint(1,20)
        while(numberExistsInPath(path, randomNum)):
            randomNum= random.randint(1,20)
        path.append(randomNum)
    population.append(path)

"""
Method to verify if the number is already in the
"""
def numberExistsInPath(path,number):
    for i in path:
        if i==number:
            return True
        return False
"""
generate the x and y arrays which represents the distances in the
x and y axis used to calculate the identity matrix in the fitness function
"""

def generateXandY():
    for _ in range(CITIES_SIZE):
        randomNumber=random.random()
        randomNumber=round(randomNumber,2)
        x.append(randomNumber)

        randomNumber=random.random()
        randomNumber=round(randomNumber,2)
        y.append(randomNumber)

"""
generates the tour matrix, which is the same matrix
"""
def generateTour():
    global tour
    tour= copy.deepcopy(population)
    for ways in tour:
        first=ways[0]
        ways.append(first)

"""
"""
def calculateDistances():
    global distances
    distances= [0 for x in range(CITIES_SIZE)]
    for i in range(len(population)):
        for j in range(len(population[i])):
            firstPos=19 if tour[i][j]==20 else tour[i][j]
            secondPos=19 if tour[i][j+1]==20 else tour[i][j+1]
            distances[i] += round(dCidade[firstPos][secondPos],4)
        dict_dist={i: distances[i] for i in range(0, len(distances))}
        distances= copy.deepcopy(dict_dist)
        return sorted(distances.items(),key=lambda kv: kv[1])

def FitnessFunction():
    for i in range(len(population)):
        for j in range(len(population)):
            dCidade[i][j]= round(math.sqrt((((x[i]-x[j])**2)+(y[i]-y[j])**2)),4)
    return calculateDistances()
    
def rouletteFunction(sorted_x):
    global parentsone
    global parentstwo
    arr=[]
    rouletteArr =[]
    for i in range(10):
        arr.append(sorted_x[i][0])
    for j in range(len(arr)):
        for _ in range(10 - j):
            parentsone=CreateParents(rouletteArr)
            parentstwo=CreateParents(rouletteArr)

    def createParents(rouletteArr):
        parentArr=[]
        for _ in range(5):
            parentArr.append(rouletteArr[random.randint(0,54)])
        return parentArr
def mutate(matrix):
    for i in range(0, len(matrix)):
        for _ in range(0,len(matrix[i])):
            ranNum=random.randint(1,100)
            if ranNum>= 1 and ranNum<=5:
                indexOne=random.randint(0,19)
                indexTwo=random.randint(0,19)
                auxOne=matrix[i][indexOne]
                auxTwo=matrix[i][indexTwo]
                matrix[i][indexOne]=auxTwo
                matrix[i][indexTwo]=auxOne

def hasDuplicity(auxArrat, usedIndexes):
    for i in range(len(auxArray)):
        for j in range(i, len(auxArray)):
            if i != j and auxArray[i]== auxArray[j]:
                if i in usedIndexes:
                    return j
                else:
                    return i
    return -1

def doCycle(sorted_x):
    global population
    children=[]

    for i in range(5):
        parentOneAux=parentsOne[i]
        parentTwoAux=parentsTwo[i]
        usedIndexes=[]

        randomIndexInsideCromossomus = random.randint(0, POPULATIO_SIZE - 1)

        usedIndexes.append(randomIndexInsideCromossomus)

        childone=copy.deepcopy(population[parentOneAux])
        childTwo=copy.deepcopy(population[parentTwoAux])

        valAuxOne=childone[randomIndexInsideCromossomus]
        valAuxTwo=childtwo[randomIndexInsideCromossomus]

        childone[randomIndexInsiderCromossomus]=valAuxTwo
        childTwo[randomIndexInsideCromossomus]=valuxOne

        while(hasDuplicity(childone, usedIndexes) !=-1):
            newIndex= hasDuplicity(childOne,usedIndexes)
            usedindexes.append(newIndexes)

            valAuxOne= childone[newIndex]
            valAuxTwo= childtwo[newIndex]

            childone[newIndex]=valAuxTwo
            childTwo[newIndex]=valAuxOne

            children.append(childOne)
            children.append(childTwo)
    mutate(children)

    tempPop= copy.deepcopy(population)

    for i in range(10):
        population[i]=copy.deepcopy(temPop[sorted_x[i][0]])
    for j in range(10, POPULATION_SIZE):
        population[j]=copy.deepcopy(children[j-10])
def name():
    
    def main():
        generateFirstPopulation()
        generateXandY()
        generateTour()

    for _ in range(NUM_EXECUTION):
        sorted_x=fitnessFunction()
        rouletteFunction(sorted_x)
        doCycle(sorted_x)
        generateTour()
        costByExecution.append(sorted_x[0][1])

    sorted_x=fitnessFunction()

    print('Total Population: %s' % (POPULATION_SIZE))
    print('Mutation_Probability: 5%')
    print('Number of cities: %s' % sorted_x[0][1])
    print('Best_Route: %s' % population[0])

    plt.plot(tour[0])
    plt.plot(tour[0], 'ro')
    plt.axis([0,20,0,20])
    plt.show()

    plt.plot(costByExecution)
    plt.show()

if __name__ == "__main__":
    main()
    
                                    
                                    






















        
