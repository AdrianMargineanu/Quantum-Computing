# Bell

This is a test for understanding quantum computer and Q#. This program is creating and testing the Entaglement of the qbits.

## Requirement
For running this code you will need The Quantum Development Kit and can be used either with the Visual Studio 2017 integrated development environment, or a development editor such as Visual Studio Code. Alternatively, the Quantum Development Kit can be used with the command line directly. You cand find the steps for installing the Quantum Developtment Kit:
*for Visual Studio 2017 [here](https://docs.microsoft.com/en-us/quantum/install-guide/vs-2017?view=qsharp-preview)
*for Visual Studio Code [here](https://docs.microsoft.com/en-us/quantum/install-guide/vs-code?view=qsharp-preview)
*for Command Line [here](https://docs.microsoft.com/en-us/quantum/install-guide/command-line?view=qsharp-preview)
## Runnig 
To run this program you will need to download the download the map Bell. Open the code using Visual Studio 2017 and just hit 'F5' or, if you are using Command Line/Visual Studio Code write the the following commands
`````````````
	$ cd Bell
	$ dotnet run
`````````````
## Explanation 
Q# is a language used for expressing quantum algorithms. This means you will need a program that simulates qbits. This is why you need Driver.cs, wich will hold the C# driver for your quantum code. Your code is in file Bell.qs

### Main Q# code 
Q# is similar to C# so first of all we need to have 
``````````````````````````````````````
namespace Quantum.Bell
{
	Open Microsoft.Quantum.Canon;
	Open Microsoft.QUantum.Primitive;
}
``````````````````````````````````````
This are 2 Q# libraries reference.Now we write the operetions. I have 2 operations : Set and BellTest.

#### Operation Set 
`````````````````````````````````````````````````
operation Set (desired: Result, q1: Qubit) : Unit
{
    let current = M(q1);
    if (desired != current)
    {
        X(q1);
    }
}
`````````````````````````````````````````````````
This operation is setting the qbit to the known state. Variable 'current' is saving the current valiue of the qubit with 'M()'. If this state is different from the state we want, it will applie 'X()' operation, that will change the state.

#### Operation Bell test
````````````````````````````````````````````````````````````````````
 operation BellTest (count : Int, initial: Result) : (Int, Int, Int)
    {
        mutable numOnes = 0;
        mutable agree = 0;
        using (qubits = Qubit[2])
        {
            for (test in 1..count)
            {
                Set (initial, qubits[0]);
                Set (Zero, qubits[1]);

                H(qubits[0]);
                CNOT(qubits[0], qubits[1]);
                let res = M (qubits[0]);
                
                if (M (qubits[1]) == res) 
                {   
                    set agree = agree + 1;
                }

                if (res == One)
                {
                    set numOnes = numOnes + 1;
                }
            }

            Set(Zero, qubits[0]);
            Set(Zero, qubits[1]);
        }
        return (count-numOnes, numOnes, agree);
    }
````````````````````````````````````````````````````````````````````
This operation is testing the superposion of the qbits and if there is an Entanglement between the qbits.We will test it in a 'for' for 'count' times. First of all we set a qbit that is 'initial' state and the second qbit to 'Zero' state. We applie the 'H()' operation on the first qbit, this means that it will be an equal probability to be 0 or 1. Then we use the 'CNOT()' operation on both of qbits. This operation is used to make Entanglemant this means that if qubits[0] is 0 the second one is for sure 0, and if qubits[0] is 1 the second one is 1. Then we verify. First if is counting how many times the state of qubits[0] is equal to qubits[1]. Second if is counting the numbers of state 1. The result of the operation is number of times the state was 0 for the qubits[0]  ('count-numOnes'), how many times it was 1 ('numOnes'), and how many times the state of the qubits was indetical ('agree'). After every test we reset both qbits on zero

### Drive.cs
I will not explain in details C#, because this is not my scope. What we need to understand that this code is a driver thats helps you to se the resault of the Q# code. We the class 'QuantumSimulator' class that expose the quantum simulator. To execuit it we need to pass 'Run' method to the quantum operation you want to execuit.
`````````````````````````````````````````````````````````````````
 using (var qsim = new QuantumSimulator())
{
    Result[] initials = new Result[] { Result.Zero, Result.One };
    foreach (Result initial in initials)
    {
        var res = BellTest.Run(qsim, 1000, initial).Result;
        var (numZeros, numOnes, agree) = res;
        System.Console.WriteLine(
            $"Init:{initial,-4} 0s={numZeros,-4} 1s={numOnes,-4} agree={agree,-4}");
    }
}
`````````````````````````````````````````````````````````````````
In our chase it is running 1000 times the code of Q# for init 'Zero' and 1000 for init 'One' and it is showing the results of it.

## Results
The results of runnig should be like this:
````````````````````````````````````
Init:Zero 0s=511  1s=489  agree=1000
Init:One  0s=516  1s=484  agree=1000
````````````````````````````````````
As we see in both cases qubit[1] state is equal to qubit[0]. Also in both cases the qubit[0] has not the same amount of 0s and 1s. This is happening because quantum pshysics is complicated. Even if we try to make the chase of both state equal it will never be equal.

Running the second test will chage some resuslts because quantum psysics is not so exact this is why is fun.