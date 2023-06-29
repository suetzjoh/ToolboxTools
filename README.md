# ToolboxTools

This project provides tools to read and write files in the [Toolbox](http://www-01.sil.org/computing/toolbox/) format. 

Work in progress

# Usage

The script can be imported and used with the following code:

	import importlib.util
	
	spec = importlib.util.spec_from_file_location("ToolboxTools.toolbox", "<Path to toolbox.py>")
	ToolboxTools = importlib.util.module_from_spec(spec)
	sys.modules["ToolboxTools.toolbox"] = ToolboxTools
	spec.loader.exec_module(ToolboxTools)

	TBProject = ToolboxTools.ToolboxProject(sys.argv[1:])

# Funding 

Funded by the Deutsche Forschungsgemeinschaft (DFG, German Research Foundation) – [SFB 1412](https://sfb1412.hu-berlin.de/), 416591334.