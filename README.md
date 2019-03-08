# Do neural networks dream of recursive sheep?

## A Lovecraftian sculpture series

Use all_files.txt as the training dataset. It contains approximately 80 STL files, converted into text form and compiled together into the one file.


## Practical Pytorch Python scripts


Run `train.py` with a filename to train and save the network:

```
> python train.py shakespeare.txt

Training for 2000 epochs...
(10 minutes later)
Saved as shakespeare.pt
```

Above, the model is saved a shakespeare.pt

In my set, the training data is called all_files.txt and the saved model is all_files.pt

After training the model will be saved as `[filename].pt` &mdash; now run `generate.py` with that filename to generate some new text:

```
> python generate.py shakespeare.pt --prime_str "Where"

Where, you, and if to our with his drid's
Weasteria nobrand this by then.

AUTENES:
It his zersit at he
```

### Training options

```
Usage: train.py [filename] [options]

Options:
--n_epochs         Number of epochs to train
--print_every      Log learning rate at this interval
--hidden_size      Hidden size of GRU
--n_layers         Number of GRU layers
--learning_rate    Learning rate
--chunk_len        Length of chunks to train on at a time
```

### Generation options

In my terminal, in the appropriate enviornment, I use the code line: 

python generate.py all_files.pt —prime_str “solid CATIA STL” —predict_len “150000” > newanimal.txt

This generates the text form of an STL file, based on the model I trained. It starts from "solid CATIA STL," the opening line in every readable STL file, and predicts the framework and vertices of the file for 150,000 characters--this is the average length of the training STL animal files.

It then automatically writes this data into a new text file, that is here named "newanimal", instead of producing this text in your terminal.

```
Usage: generate.py [filename] [options]

Options:
-p, --prime_str      String to prime generation with
-l, --predict_len    Length of prediction
-t, --temperature    Temperature (higher is more chaotic)
```

### A note:

As of this commit (3/8/19) the moel generates the entire framework of the STL, not just the vertices. This has the result that the model wil NOT generate "end CATIA STL", the last line of a readable STL file, and will often stop generating in the middle of a block (look at the camel or cat text to see what the structure should be).

To make the file readable, I delete the mid-sentence part at the end of the generated file, then add "end CATIA STL", following the most recent "end loop" command. Then you can change the file type from "txt" to "stl" to see if you've generated a visible/physical structure.
