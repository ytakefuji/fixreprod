# fixreprod
This is under review.

fixreprod is to able to show all seeds which are needed to be fixed in AI systems.

To run fixreprod, install it by the following commanad. ($) indicates the prompt from the system in the terminal.

$ pip install fixreprod

# How to run fixreprod

For example, assume cartpole_reinforce.py is a source code. Use grep command to generate test.py.
test.py contains imported libraries which will be checked by fixreprod.

$ grep import cartpole_reinforce.py >test.py

Before running fixreprod, you must install all libraries used in the source code.
In cartpole_reinforce.py, gym, random, numpy, and torch must be installed.

<pre>
Run fixrepdod and enter "test.py" for checking.
fixreprod will show the all seeds to be fixed to eliminate 
reproducibility problems from your code. 14 seeds are shown in this example.
  
$ fixreprod
Enter the source code file name: test.py
gymnasium.Space.seed(13123)
gym.Space.seed(80245)
random.Random.seed(82744)
random.SystemRandom.seed(40572)      
random._inst.seed(53626)
numpy.random.seed(71207)
torch.Generator.seed(61874)
torch.default_generator.seed(65692)  
torch.random.seed(57377)
torch.cuda.seed(78878)
torch.torch.seed(70766)
torch.ops.seed(4417)
torch.classes.seed(88108)
torch.nn.functional.torch.seed(35587)

</pre>
