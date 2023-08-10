# ToolboxTools

This project provides tools to read and write files in the [Toolbox](https://software.sil.org/toolbox/) format. 

Work in progress

# Usage

## input data

This script operates on Toolbox projects which are built around the file 'Toolbox.prj'. They consist of a folder with an arbitrary structure that contains all files relevant to the project. A blank project can be downloaded from the [documentation website](http://www.fieldlinguiststoolbox.org).

## output data

The output files will be generated in your working directory, thus it is advised that you don't put the Toolbox folder into the same directory as the script.

## import

The script can be imported and used with the following code:

	import importlib.util
	
	spec = importlib.util.spec_from_file_location("ToolboxTools.toolbox", "<Path to toolbox.py>")
	ToolboxTools = importlib.util.module_from_spec(spec)
	sys.modules["ToolboxTools.toolbox"] = ToolboxTools
	spec.loader.exec_module(ToolboxTools)

	TBProject = ToolboxTools.ToolboxProject(sys.argv[1:])
	
## arguments

| argument | description |
| -------- | ----------- |
| '-r' | This argument has to be passed, if you want to reload the data from your Toolbox project. You can add '["-r"]' to the start of the array that is passed when calling 'ToolboxTools.ToolboxProject()'. If this argument is not passed, the script will reuse the data from the last import that has been stored in your working directory under the name '(YOUR_PROJECT_NAME)_annotation.csv'. |

The last argument should be the path to the Toolbox folder. Alternatively to submitting the path via the command line you can use a keyword that is defined in 'config.txt'. To define a keyword, simply add a line that consists of the keyword (or multiple comma-separated keywords) and a path, both separated from each other by a single space. If no path is given, the script will not execute.

# Funding 

Funded by the Deutsche Forschungsgemeinschaft (DFG, German Research Foundation) – [SFB 1412](https://sfb1412.hu-berlin.de/), 416591334.