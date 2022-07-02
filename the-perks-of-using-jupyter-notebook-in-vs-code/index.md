# The Perks of using Jupyter Notebook in VS Code


Why and how to use Jupyter Notebooks in VS Code

## 1 Introduction

It’s no secret that Jupyter Notebook is the go-to IDE in the data science field. The cell nature of Jupyter allows instant running of a block of code snippet and manifest of the output.

{{< image src="editor1.jpeg" caption="Photo by the author" >}}

It works seamlessly well with the nature of data analysis operation, specifically in the way where the subsequent lines of code highly depend on the scrutinization of the current cell output.

While using Jupyter Notebook is great by itself, the features can be greatly enhanced when used in VS Code with the Jupyter Extension.

## 2 Why use Jupyter Notebooks in VS Code?

1. Shallow learning curve

To begin with, a developer had utilized VS Code at some point in code development. Hence, there is a very shallow learning curve to start using Jupyter notebooks in VS Code.

{{< image src="vscode.png" caption="Photo by the author" >}}

2. Seamlessly swaps between files of different format

{{< image src="filedirec.jpg" caption="Photo by the author" >}}

A project folder, in general, contains files of different formats. For example, python notebooks(.ipynb) are used for data analysis and modeling steps, while native python scripts(.py) are preferred when deploying models. Not to mention there are also sources of data input and output in the form of CSV or excel.

By setting VS Code as the go-to-workspace, alternating between files is effortless. Subsequently editing each file can be done side by side with the optimized view being presented according to the file format. VS Code works especially well with markdown files as shown below.

{{< image src="editor2.jpeg" caption="Photo by the author" >}}

3. Built-in terminal in VS Code

The ability to open a terminal in the VS Code itself is especially useful. With this feature, one can run git operations and other text-based commands in the same interface.

{{< image src="editor3.jpeg" caption="Photo by the author" >}}

This truly shows the powerful features in VS Code to allow day-to-day operations to be carried out in an all-in-one platform.

## 3 How to user Jupyter Notebooks in VS Code?

As the layout for Jupyter in VS Code varies compared to native web browsers, this section introduces 4 fundamental functionalities to ensure an easy adoption for Jupyter Notebook in VS Code.

- Install Jupyter extension
- Create Jupyter notebook
- Change Conda environment
- Change cell type

### 3.1 Install Jupyter Extension

Installing of Jupyter extension provides notebook support in the IDE.

1. Run VS Code, and open up Extension View by either

- Clicking on the Extensions icon in the Activity Bar, or

{{< image src="vscode1.jpeg" caption="Photo by the author" >}}

- Using shortcut keys (Ctrl+Shift+X)

2. Search with the keyword **Jupyter** and install the first option in the list.

{{< image src="vscode2.jpeg" caption="Photo by the author" >}}

### 3.2 Create Jupyter Notebook

There are two methods to create a new Jupyter Notebook.

- Open the command palette with shortcut keys (Ctrl + Shift + P). Search for **Jupyter: Create New Jupyter Notebook**

{{< image src="editor4.jpeg" caption="Photo by the author" >}}

- Click on the new file icon, and name the new file ends with _.ipynb_ extension

{{< image src="editor5.jpeg" caption="Photo by the author" >}}

### 3.3 Change Conda Environment

To select Conda virtual environment for the notebook, simply click on the environment tab in the top right corner. Subsequently, select the desired environment from a drop-down list of Conda environments.

{{< image src="editor6.jpeg" caption="Photo by the author" >}}

Do take note that this step is performed with a notebook opened in VS Code.

### 3.4 Change cell type

To change the cell type of any cell, simply click on the tab located at the bottom right of the cell. A drop-down list of cell types will appear for selection.

{{< image src="editor7.jpeg" caption="Photo by the author" >}}

Here, the most fundamental operations to use Jupyter Notebooks in VS Code are introduced. These 4 functionalities are sufficient for most of the daily usages.

Check out [VS Code documentation](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) for other functionalities in mind.

---

Do take note that some time is needed to get familiarized with the interface. This is especially true if the user has been using Jupyter notebook in the native browser. Yet, the learning shall not possess any major difficulties and can be polished with frequent usages.

Thanks for reading! I hope you experience a boost of productivity with this setup!

