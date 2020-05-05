# Bonjour!

Voici un petit programme python d'analyse combinatoire. 
Il permet de calculer les arrangements et les combinaisons de k parmi n pour des valeurs dépassant les capacités d'une calculatrice.

```python runnable
def A(k, n):
    """Nombre d'arrangements sans répétition de k objets pris parmi n"""
    x = 1   
    i = n-k+1
    while i <= n:
        x = x*i
        i += 1
    return x

def fact(n):
    """Nombre de permutation de n objets"""
    return A(n,n)

def C(k, n):
    """Nombre de combinaisons sans répétition de k objets pris parmi n"""
    if k > n//2:
        k = n-k
    x = 1
    y = 1
    i = n-k+1
    while i <= n:
        x = (x*i)//y
        y += 1
        i += 1
    return x

def gamma(k, n):
    """Nombre de combinaisons avec répétitions de k objets pris parmi n"""    
    return C(k, n+k-1)

def listA(k, S):
    """Liste les arrangements sans répétition de k lettres prises parmi les lettres de S"""
    x = [] 
    if k == 1:
        for c in S:
            x.append(c)
        return x  
    l = len(S)
    for i in range(l):
        xi = S[i]
        Si = S[:i]+S[i+1:]
        #print(Si)
        Ai = listA(k-1, Si)
        #print(Ci)
        for ai in Ai:
            x.append(xi+ai)
    return x

def listC(k, S):
    """Liste les combinaisons sans répétition de k lettres prises parmi les lettres de S"""
    x = [] 
    if k == 1:
        for c in S:
            x.append(c)
        return x  
    l = len(S)
    for i in range(l-k+1):
        xi = S[i]
        Si = S[i+1:]
        #print(Si)
        Ci = listC(k-1, Si)
        #print(Ci)
        for ci in Ci:
            x.append(xi+ci)
    return x


def listGamma(k, S):
    """Liste les combinaisons avec répétition de k lettres prises parmi les lettres de S"""
    x = [] 
    if k == 1:
        for c in S:
            x.append(c)
        return x  
    l = len(S)
    for i in range(l):
        xi = S[i]
        Si = S[i:]
        #print(Si)
        Gi = listGamma(k-1, Si)
        #print(Gi)
        for gi in Gi:
            x.append(xi+gi)
    return x

print(A(3,5))
print(listA(3, 'abcde'))
print(C(3,5))
print(listC(3, 'abcde'))
print(gamma(3,5))
print((listGamma(3, 'abcde')))
print((listGamma(5, 'fp')))
```

# Exercice

Ajouter une instruction en fin de programme pour calculer le nombre de combinaisons de 19 parmi 67
