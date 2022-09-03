# Artifical-Intelligence
# Deepth First Search(DFS) Algorithm
class Graph:

    def __init__(self, count):      #----------Initialization
        self.count=count
        self.mydict={}
        # print(self.mydict)

    def solution(self, node1, node2):      #-----------Making Graph
        if node1 not in self.mydict:            #------If set for node is not present (1/3)
            self.mydict[node1] = set()          #------then create one and add neighbour (2/3)
            self.mydict[node1].add(node2)       #------nodes in that set (3/3)
        else:                                   #------Else add neighbour in already present set
            self.mydict[node1].add(node2)

    def DFS(self, start, target, que=[], visited=[]):   #-----DFS method
        self.visited= visited       
        visited.append(start)           # ----------Adding start node to visited
        # print(f'VISITED:{visited}')
        while start not in que:
            que.append(start)           # ----------Adding start node to Que
        if start==target:
            que.remove(start)
            # print(f'QUE:{que}')
            print("Gotcha")             #-----------When DFS find the goal node
            print(f'VISITED:{visited}')
        else:
            que.remove(start)               #---------------Removing start node as it is visited
            if start not in self.mydict:    #---------------When a node doesn't have neighbour
                print(f"{start}: has no neighbour")
            else:    
                for neighbours in self.mydict[start]:       #--------Arranging Que
                    # print(neighbours)
                    while neighbours not in que:                        
                        que=[neighbours]+que
                        
            for i in que:           #-------Used to avoid continues loop due to same node in que
                if i==start:        #-------1
                    que.remove(i)   #-------2   
            print(f'QUE:{que}')     # -----------Printing Que
            self.DFS(que[0], target, que, visited)   #--------Iterating method for every neighbour node
            
    def printing(self):             #----------Printing
        # print(self.Path)
        print(self.mydict)
        # print(f'Vsited:{self.visited}')
        # for i in self.mydict:
        #     print(f'Node-{i} : {self.mydict[i]}')


g = Graph(5)

g.solution('a','a')
g.solution('a', 'b')
g.solution('a', 'c')
g.solution('b', 'e')
g.solution('b', 'd')
g.solution('e', 'f')
g.solution('e', 'g')

l_path = g.DFS('a', 'g')
# print(f"Path:{l_path}")

g.printing()
