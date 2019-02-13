## Introduction
The computer has change a lot since its first apparition. It became smaller and more powerfull. The smaller it becomes, the more influenced by [quantum physics](https://www.sciencedaily.com/terms/introduction_to_quantum_mechanics.htm) is. This means that if a transistor doesn`t allow an electron to go any further,the electron, can transfer itself by a proces call [quantum tunneling](https://www.azoquantum.com/Article.aspx?ArticleID=12). This is happening because, classic physics is no longer applied in, on a quantum scale , this means 100 nanometers. So in '80s was initiated the field of quantum computing. ![quantum](/Imagies/qP.png)
  
## Qbits 
Classic computer works on bits, that has 2 basic states. In a quantum computer we have qbits, that can be an electron’s internal angular momentum, or spin, which has the peculiar quantum property of having only two possible projections on any coordinate axis: +1/2 or –1/2 (in units of the [Planck's constant](https://whatis.techtarget.com/definition/Plancks-constant)). This means you have 2  basic states, as well: ↑ (that can be used as 0) and ↓ (that can be used as 1, because you need energy to make this electron to be in such state). 
This spin state is described by a formula that includes 2 complex numbers, let`s say α and β, wich are called [quantum amplitudes](https://en.wikipedia.org/wiki/Probability_amplitude). The rules of quantum mechanics say that the square of this numbers must add up to 1 and the square of this numbers is the probability of finding this electron in this state. Why probability of finding? Because quantum physics has something called [superposion](http://www.physics.org/article-questions.asp?id=124), this means that the electron has both states at the same time but when you look at it is showing one of them.![real](/Imagines/mustbe.png)

When you have a system of 2 qbits you need 4 complex numbers ,that square of them must add up to 1. In general, if you have a system of N qbits you would have 2 powered N amplitudes, and this is the power of the quantum computer. In other words, if you have a computer of 64 bits, it is as strong as a quantum computer of 6 qbits. 
With the help of [entaglement phenomenon](https://www.sciencedaily.com/terms/quantum_entanglement.htm), which means that all qbits depend one on another, you can look at the position of the first electron and calculate the position of all others.
Quantum gates work different from normal gates. It has the income of a superposion and changes it to another superposition. Basically an electron can be described by 3 vectors in space. These gates change this vectors, but we are talking about superposition, so these gates manipulate the probabilites of the qbits state. The output of the the gate is another superposition.

## Utilites 
This new type of computer can be helpful in some areas, like: security,science and another aereas where you have a large time of running a program beacuse a quantum algorithm can run it in square root of that time. 
### Science 
Simulations are very important for new discoveries. Usually they are made on computers and it takes a lot of time. Because are a lot of variables that have to be calculated for a more accurate result. Quantum computers are working exponentially faster.
### Security
The biggest problem in security of modern computers is internet, that can provide (in some situations) information leak. This is not a problem when, with the help of entaglement phemenon, the infomarmation is not transmited physically but on a quantum level. This means that this electron and the other electron (it does not matter if that electron is on the moon) are interecting with each other and if know in what state is this electron I know in which state is the other electron. In this way you can communicate. 

## Conclusion
This new type of computer can change the world, but it will not be the replacement for our classic computer. The algorithm of the quantum computers is very complicated, and doing simple tasks will not make the it faster. Some timed it can make even slower that digital computer. When it comes to really big algorithms that take some time this is where you need this type of computer, especially when you know that building such a computer is very hard.

## Development
This kind of technology built by a lot of companies like: Microsoft, Google, IBM, Intel. IBM made an online platform that allows the users to test a quantum algorithm on their prototype of quantum computer which is called [IBM Q](https://quantumexperience.ng.bluemix.net/qx/experience). This computer has 3 processors: 2 of 5 qbits and one of 16 qbits. 
And Microsoft made a programing language called [Q#](https://www.microsoft.com/en-us/quantum/development-kit)( Q-sharp ), that helps you to simulate a programme as if it is on 30 qbits or 40 if you use Azure. So you can experience the quantum computer by yourself. I coded a little programme in Q# to test the entanglement of qubits. You can find it [here](https://github.com/playerjack/Quantum-Computing/tree/master/Bell). 
   

