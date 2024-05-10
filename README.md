# ToolboxTools

This project provides tools to read and write files in the [Toolbox](https://software.sil.org/toolbox/) format. 

# Usage

## import

The script can be imported and used with the following code:

	import importlib.util
	
	spec = importlib.util.spec_from_file_location("ToolboxTools.toolbox", "<Path to toolbox.py>")
	ToolboxTools = importlib.util.module_from_spec(spec)
	sys.modules["ToolboxTools.toolbox"] = ToolboxTools
	spec.loader.exec_module(ToolboxTools)

	TBProject = ToolboxTools.ToolboxProject(sys.argv[1:])
	
## input data

This script operates on Toolbox projects which are built around the file `Toolbox.prj`. They consist of a folder with an arbitrary structure that contains all files relevant to the project. A blank project can be downloaded from the [documentation website](http://www.fieldlinguiststoolbox.org).

## output data

The default folder for the output is a sister directory to your Toolbox folder with the name `YOUR_PROJECT_NAME-log`. As of version 1.1 (March 24) the output folder for the log and csv export can be set manually via: 

```
TBProject.set_export_path(PATH)
TBProject.set_excel_path(PATH)
```

The export will also no longer be executed automatically if the necessary arguments are provided. Instead you have to call the function `TBProject.write_toolbox_project()`. This is to ensure that no data will be exported into an unintended location.
	
## arguments

| argument | description |
| -------- | ----------- |
| `-r` | This argument has to be passed, if you want to reload the data from your Toolbox project. You can add `["-r"]` to the start of the array that is passed when calling `ToolboxTools.ToolboxProject()`. If this argument is not passed, the script will reuse the data from the last import that has been stored in your working directory under the name `YOUR_PROJECT_NAME_annotation.csv`. |
| `--db` | This argument has to be passed in order to load the databases that are used by Toolbox to store the possible annotations. If `-c` is passed, this argument is not necessary. |
| `-p` | The “print” argument will lead to your Toolbox files being reexported into a subdirectory in your working directory with the same name as your Toolbox folder. Independently of the reexport, a csv file with your annotation will always be generated in your working directory. |
| `--as-one` | If this argument is passed, the reexported Toolbox files will be combined in a single file with the same name as your Toolbox folder. |
| `-f` `FILTER` | In order to filter the range of data that is loaded into the Toolbox project you can use a file called `filter.csv` in your Toolbox folder. The filter is based on your ref-marker. For this to work your ref-marker should follow the structure `CORPUSNAME_PART_PAGE.LINE` where `PART` can be an arabic or roman numeral (capital letters). In your `filter.csv`, add a line with the structure `CORPUSNAME_PART_;PAGE.LINE_MIN;PAGE.LINE_MAX;FILTER_ID` (Compare the function `is_in_subpart_`). Then pass the filter IDs that you want to include joined by a comma to the `-f` argument. The filter will affect the contents of all files exported. |
| `-c` | The “check” argument will lead the Script to evaluate the annotation of your Toolbox corpus based on the databases that are used to store all possible annotations by Toolbox. Not up-to-date Annotations will be corrected on the spot if there is not more than one possible annotations. All changes and inconsistencies are logged in a file called `YOUR_PROJECT_NAME_log.csv`. | 
| `--ignore-numbers` | This argument will make the script ignore all tokens that are exclusively digits, as Toolbox itself does. |
| `--strict` | This argument will lead to all tokens that are not matched by database entries to be removed from the annotation. This can be used to gauge how much of your text has been annotated. | 
| `--reload=` `PATH` | This argument can be used to reload the text data of your Toolbox project from an xml-file that contains the full text. This functionality is currently under construction. |
| `--reload-only=` `REGEX` | If this argument is passed, only tokens that match the regex will be loaded into the Toolbox project from the xml-file. |
| `-e` `FILENAME` | The “excel” argument can be used to export the content of the `YOUR_PROJECT_NAME_annotation.csv` into an xlsx-file. It is not functional on it's own, because the exact definition of the function depends on your particular project. It's main function is to set the value of the boolean `TBProject.Is.excel_export` for you to implement a conditional export. The export path will be available in the attribute `TBProject.excel_export_path`.|
| `-z` | This argument is specific to the project [B02](https://sfb1412.hu-berlin.de/projects/b02/) of the SFB 1412. |

The last argument should be the path to the Toolbox folder. Alternatively to submitting the path via the command line you can use a keyword that is defined in `config.txt`. To define a keyword, simply add a line that consists of the keyword (or multiple comma-separated keywords) and a path, both separated from each other by a single space. If no path is given, the script will not execute.


# Funding 

Funded by the Deutsche Forschungsgemeinschaft (DFG, German Research Foundation) – [SFB 1412](https://sfb1412.hu-berlin.de/), 416591334.

This software was used to modify the data for  the _grammatically annotated corpus of the pericopes of the Old Lithuanian Postil of Jonas Bretkūnas_ (DOI: [10.5281/zenodo.7890990](https://doi.org/10.5281/zenodo.7890990)) and the _Grammatically Annotated Corpus of the Old Latvian Postil of Georg Mancelius_ (DOI: [10.5281/zenodo.7890894](https://doi.org/10.5281/zenodo.7890894)).