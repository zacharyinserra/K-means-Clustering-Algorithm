import math
import matplotlib.pyplot as plt
import random

plt.ion()

centroidNum = 5
centroids = []
points = []

class Point(object):
    def __init__(self, x, y, cl, color):
        self.xCoord = float(x)
        self.yCoord = float(y)
        self.cla = cl
        self.color = color
        points.append(self)

    def __repr__(self):
        return "("+str(self.xCoord)+", "+str(self.yCoord)+")"

    def getX(self):
        return self.xCoord
    def getY(self):
        return self.yCoord
    def getCl(self):
        return self.cla
    def setCl(self, clas):
        self.cla = clas
    def getColor(self):
        return self.color
    def setColor(self, color):
        self.color = color

def plotPoints():
    for i in points:
       plt.scatter(i.getX(), i.getY(), color=i.getColor(), marker=i.getCl(), alpha=0.5)
    for i in centroids:
        plt.scatter(i[0], i[1], c = 'black', marker = 'x')
    plt.axis([0, 1, 0, 1])
    plt.title("Training Data")
    plt.xlabel("x")
    plt.ylabel("y")
    plt.show()

def genCentroids():
    for i in range(centroidNum):
        x = random.uniform(0, 1)
        y = random.uniform(0, 1)
        centroids.append((x, y))

'''Find closest centroid for each data point'''
'''Assign data point to that centroid'''
def assignment(points, centroids):
    dist = []
    sumX = [0,0,0,0,0]
    sumY = [0,0,0,0,0]
    count = [0,0,0,0,0]
    for i in points:
        for j in centroids:
            dist.append(math.hypot(i.getX() - j[0], i.getY() - j[1]))
        shortestD = dist.index(min(dist))
        sumX[shortestD] += i.getX()
        sumY[shortestD] += i.getY()
        count[shortestD] += 1
        '''Shortest distance is centroid for assignment'''
        '''Example: if == 0, point belongs to cluster 1'''
        if shortestD == 0:
            i.setCl("<")
            i.setColor('blue')
        elif shortestD == 1:
            i.setCl(">")
            i.setColor('red')
        elif shortestD == 2:
            i.setCl("^")
            i.setColor('green')
        elif shortestD == 3:
            i.setCl('s')
            i.setColor('purple')
        else:
            i.setCl('o')
            i.setColor('orange')
        dist.clear()
    cond = updateCentroid(centroids, sumX, sumY, count)
    plotPoints()
    return cond

'''Updates centroid locations and point assignment'''
def updateCentroid(centroids, sumX, sumY, count):
    oldCentroids = []
    for i in range(len(centroids)):
        newCentroid = (sumX[i]/count[i], sumY[i]/count[i])
        oldCentroids.append(centroids[i])
        centroids[i] = newCentroid
    if centroids == oldCentroids:
        return True
    else:
        return False

inFile = open('Data', 'rt')
cl = 'o'
color = 'purple'
for line in inFile:
    Point(line.split(",")[0], line.split(",")[1], cl, color)
inFile.close()

updates = 0
genCentroids()
plotPoints()
switch = False
while not switch:
    switch = assignment(points, centroids)
    updates += 1

print("Convergence reached in " + str(updates) + " updates")