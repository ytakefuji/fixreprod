# fixreprod
This is under review.

It is still undergoing improvement.

fixreprod is an indispensable tool to solve reproducibility problems in pseudorandom numbers by fixing all seeds and deterministic algorithms used in libraries of AI systems.

To run fixreprod, install it by the following command. ($) indicates the prompt from the system in the terminal.

$ pip install fixreprod

# How to run fixreprod

For example, assume reinforcement_q_learning.py is a source code. Use grep command to generate test.py.
test.py contains imported libraries which will be checked by fixreprod. The sed command sed '/^"""/,/^"""/d' removes comment lines from reinforcement_q_learning.py and saves it in reinfo.py. The first grep command removes comment lines with the first character of "#" from reinfo.py and save it in rein.py. The second grep command extracts imported libraries from rein.py and save it in test.py.

$ grep import reinforcement_q_learning.py >test.py

or To see the code only, run the following commands

$ sed '/^"""/,/^"""/d' reinforcement_q_learning.py >reinfo.py

$ grep -v '^#' reinfo.py >rein.py

$ grep import rein.py >test.py

Before running fixreprod, you must install all libraries used in the source code.
In reinforcement_q_learning.py, gym, random, numpy, and torch must be installed.

<pre>
Run fixrepdod and enter "test.py" for checking.
fixreprod will show the all seeds to be fixed to eliminate 
reproducibility problems from your code. 
9 seeds and 1 fixing deterministic algorithms are found 
  in this example.
  
$ fixreprod
Enter the source code file name: test.py
env.action_space.seed(0)
env.reset(seed=0)
np.random.seed(0)
random.Random().seed(0)
random.seed(0)
torch.Generator().manual_seed(0)        
torch.cuda.manual_seed(0)
torch.cuda.manual_seed_all(0)
torch.manual_seed(0)
torch.use_deterministic_algorithms(True)

</pre>
These generated codes should be inserted in the rein.py. The result is shown in the following.

<img src='https://github.com/ytakefuji/fixreprod/raw/main/result.png' width=540 hight=480>
