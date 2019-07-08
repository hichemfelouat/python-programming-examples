# -*- coding: utf-8 -*-
"""
@author: Hichem Felouat
"""

import networkx as nx
import numpy as np

def adjacency_matrix(nbr_nodes,lst_edges):
    M = np.zeros((nbr_nodes,nbr_nodes)) 
    for i in lst_edges :
        M[i[0]][i[1]] = 1
        M[i[1]][i[0]] = 1
            
    return M
    
    
def isInlst (L,v):
    for i in range(len(L)):
        if L[i] == v :
            return 1
    return 0
    
def maxIndVal(L):
    ind_max = 0
    val = L[0]
    for i in range(len(L)):
        if L[i] > val :
            ind_max = i
            val = L[i]
    return ind_max,val
    
    
def BC1E(paths,lst_edges,source):
    nbr_nodes = len(paths)
    M = adjacency_matrix(nbr_nodes,lst_edges)
    
    lst_levels =[]
    for i in range(nbr_nodes):
        lst_levels.append(0)
        
    lst_levels[source] = 1
    lst_levels_tmp = []
    for i in range(nbr_nodes):
        if M[source][i] == 1 :
            lst_levels[i] = 1
            lst_levels_tmp.append(i)
            
    lst_nodes_fine = [] 
    lst_nodes_fine.append(source)   
    while len(lst_nodes_fine) < nbr_nodes :
        ind = lst_levels_tmp[0]
        
        for i in range(nbr_nodes):
            if M[ind][i] == 1 and isInlst (lst_nodes_fine,i)==0:
                lst_levels[i] = lst_levels[i] + lst_levels[ind]
                if isInlst (lst_levels_tmp,i)==0 :
                    lst_levels_tmp.append(i)
                    
        lst_levels_tmp.remove(ind)        
        lst_nodes_fine.append(ind)  
        
    print(paths)
    print('Levels :')
    print(lst_levels)
    print('Edges :')
    print(lst_edges)    
    #**********************
    lst_d = []
    lst_f = []
    lst_val =[]
    lst_BC_edges = []
    for i in range(nbr_nodes):
        lst_val.append(0)
        
    for i in range(len(lst_edges)):
        lst_BC_edges.append(0)
    
    indf,valf = maxIndVal(lst_levels)
    lst_val[indf] = valf
    
    for i in range(nbr_nodes):
        if M[indf][i] == 1 :
            bc = float(lst_levels[i]) / float(valf)
            for j in  range(len(lst_edges)) :
                e = lst_edges[j]
                if (e[0]==indf and e[1]== i) or (e[0]==i and e[1]== indf) :
                    lst_BC_edges[j] = bc
                    lst_val[i] = lst_val[i] + bc
                    if isInlst (lst_d,i)== 0 :
                        lst_d.append(i)
               
    lst_f.append(indf)
    while len(lst_d) > 0 : 
        ind = lst_d[0]
        cpt = 0
        for i in range(nbr_nodes):
            if M[ind][i] == 1 and isInlst (lst_f,i)== 0:
                cpt = cpt + 1
        if cpt == 0 :
            cpt = 1
        bcp = float(lst_val[ind]) / float(cpt)
        for i in range(nbr_nodes):
            if M[ind][i] == 1 and isInlst (lst_f,i)== 0:
                bc = (float(lst_levels[i]) / float(lst_levels[ind])) + float(bcp)
                for j in  range(len(lst_edges)) :
                    e = lst_edges[j]
                    if (e[0]==ind and e[1]== i) or (e[0]==i and e[1]== ind) :
                        lst_BC_edges[j] = bc
                        lst_val[i] = lst_val[i] + bc
                        if isInlst (lst_d,i)== 0 :
                            lst_d.append(i)
                            
        lst_d.remove(ind)        
        lst_f.append(ind)
    #***********
    print('BC :')
    print(lst_BC_edges)
            
            
    
    
    
        
            
    
          
    
G=nx.Graph()

G.add_node(0)
G.add_node(1)
G.add_node(2)
G.add_node(3)
G.add_node(4)
G.add_node(5)
#----------------------
G.add_edge(0,1)
G.add_edge(0,3)
G.add_edge(1,4)
G.add_edge(1,5)
G.add_edge(3,4)
G.add_edge(4,2)
G.add_edge(5,2)
print('----------------------------------------')
print("normal")
path = nx.single_source_shortest_path(G,1)
lst_nodes = G.nodes()
lst_edges = G.edges()
BC1E(path,lst_edges,1)
nx.draw(G, with_labels = True)
