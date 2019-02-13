# Bell

This is a test for understanding quantum computer and Q#. This program is created and tests the entanglement of the qbits.

## Requirement
For running this code you will need The Quantum Development Kit and can be used either with the Visual Studio 2017 integrated development environment, or a development editor such as Visual Studio Code. Alternatively, the Quantum Development Kit can be used with the command line directly. You can find the steps for installing the Quantum Developtment Kit at the following links:
* for Visual Studio 2017 [here](https://docs.microsoft.com/en-us/quantum/install-guide/vs-2017?view=qsharp-preview)
* for Visual Studio Code [here](https://docs.microsoft.com/en-us/quantum/install-guide/vs-code?view=qsharp-preview)
* for Command Line [here](https://docs.microsoft.com/en-us/quantum/install-guide/command-line?view=qsharp-preview)

## Running 
To run this program you will need to download the directory Bell. Open the code using Visual Studio 2017 and just hit 'F5', or, if you are using Command Line/Visual Studio Code, write the the following commands:
`````````````
	$ cd Bell
	$ dotnet run
`````````````
## Explanation 
Q# is a language used for expressing quantum algorithms. This means you will need a program that simulates qbits. This is why you need Driver.cs, which will hold the C# driver for your quantum code. Your code is in file Bell.qs

### Main Q# code 
Q# is similar to C# so first of all we need to have 
``````````````````````````````````````
namespace Quantum.Bell
{
	Open Microsoft.Quantum.Canon;
	Open Microsoft.QUantum.Primitive;
}
``````````````````````````````````````
These are 2 Q# reference libraries. Now we write the operations. I am ussing: Set and BellTest.

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
This operation is setting the qbit to the known state. Variable 'current' is saving the current value of the qubit with 'M()'. If this state is different from the state we want, it will apply 'X()' operation, which will change the state.

#### Operation BellTest
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
This operation is for testing the superposition of the qbits and if there is an entanglement between the qbits. We will test it in a 'for' for 'count' times. First of all we set a qbit in the 'initial' state and the second qbit to the 'zero' state. We apply the 'H()' operation on the first qbit, which means that it will have an equal probability to be 0 or 1. Then, we use the 'CNOT()' operation on both qbits. This operation is used to make the entanglement. This means that if qubits[0] is 0 the second one is for sure 0, and if qubits[0] is 1 the second one is 1. Then we verify. First, it is counting how many times the state of qubits[0] is equal to qubits[1]. Second, it is counting the how many times the state is 1. The result of the operation is the number of times the state was 0 for the qubits[0]  ('count-numOnes'), how many times it was 1 ('numOnes'), and how many times the state of the qubits was identical ('agree'). After every test we reset both qbits to zero.

### Drive.cs
I will not explain in details C#, because this is not my scope. What we need to understand, is that this code is a driver that helps you to see the result of the Q# code. We use the class 'QuantumSimulator', which exposes the quantum simulator. To execute it, we need to pass 'Run' method to the quantum operation.
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
In our case, it is running the Q# code for init 'Zero' 1000 times and another 1000 thimes for init 'One' and it is showing the results.

## Results
The results of running should be like this:
````````````````````````````````````
Init:Zero 0s=511  1s=489  agree=1000
Init:One  0s=516  1s=484  agree=1000
````````````````````````````````````
As we see in both cases qubit[1] state is equal to qubit[0]. Also in both cases the qubit[0] has not the same amount of 0s and 1s. This is happening because quantum physics is complicated. Even if we try to make the case of both states equal it will never be equal.

Running the second test will change some results because quantum physics is not so exact and this is why it is fun.