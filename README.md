
C# API for [OMX](https://github.com/osPlanning/omx)

# Development Environment
It will be easiest if you have Visual Studio 2012 Express for Windows Desktop 
installed. The solution file provided was created using this version of 
Visual Studio. It might work with different versions but it hasn't been tested yet.

# Where is the C# library for working with OMX?
The dll is located [here](https://github.com/osPlanning/omx-csharp/tree/master/src/CSharpOMX/CSharpOMX/bin/Debug)

# HDFDotNet
Before you begin any work, it is recommended that you look through the [hdf5](http://hdf5.net) site to 
familiarize yourself with how Dot Net works with HDF5.  Warning!  The HDFDotNet library and 
documentation is not well-maintained and so you will find some special puzzles when working with it.

The CSharpOMX.dll code references the HDF5DotNet dlls, and you may need reference the 
HDF5DotNet dlls if you wish to access omx files. 

# Example Test Code
This [test code](https://github.com/osPlanning/omx-csharp/tree/master/test/TestOMX/TestOMX) uses 
the CSharpOMX dll and HDFDotNet dll libraries to create and read omx files.  It can read 
in the R and Python example files referenced in their user's guides.  As you can see, 
the paths are hard-coded so you will to set them for your environment.

# Classes & Methods
The two classes are: OMXFile.cs and OMXMatrix.cs.

OMXFile
An OMXFile has the following member variables:
* private string filepath;
* private H5FileId fileID;
* public string[] omxVersion = { "0.2" };
* private H5GroupId rootGroup;
* private long[] shape;
* private string rootGroupName = "/data";
* public string omxVersionName = "OMX_Version";

The constructor for the class looks like this OmxFile(string filePath, long[] shape)

The following properties can be accessed outside the class
* RootGroupName
* OMXVersion
* Shape
* FileID

The following methods are available for use with an OMXFile.
* CreateFileOMX()
* CreateMapping(int[] tazEquiv, string mapName)
* GetMapping(string mapName)
* OverwriteCheck()
* OpenReadOnly()
* OpenReadWrite()
* OpenDebug()
* Close()

OMXMatrix
An OMXMatrix has the following member variables:
* private long[] shape;
* private H5FileId fileId;
* private H5DataSetId matrixId;
* private H5DataTypeId matrixTypeId;
* private H5DataSpaceId matrixSpaceId;
* private string groupName;
* private H5GroupId groupId;
* private string matrixName;

The constructors for the class look like this:
* OmxMatrix(OmxFile omxfile, string matrixName, H5DataTypeId matrixTypeId)
* OmxMatrix(OmxFile omxfile, string matrixName)

Use the first one if you are creating a matrix for the first time because in that case you need to send in its type.

The following property can be accessed outside the class.
* MatrixTypeId

The following methods are available for use with an OMXMatrix.
* GetInt16Matrix()
* GetDoubleMatrix()
* FillInt16Matrix(UInt16[,] memMatrix)
* GetInt16MatrixWithMap(int[] mapping, int offsetsize)
* FillFloatMatrix(float[,] memMatrix)
* CreateMatrixIfNoneExists(H5GroupId groupId, string matrixName, long[] shape, H5DataTypeId matrixTypeId, H5DataSpaceId matrixSpaceId)

