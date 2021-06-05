# ClasTool

## Requirements

* **xutils-dev**

* **ROOT**

* **gawk**

## Environment variables

In sumary, you must define the following environment variables:
* `CLASTOOL` as the current **ClasTool** directory
* `CLAS_LIB` as the current **clas_lib** directory
* `CLAS_PACK` as the current **clas_pack** directory

These next two variables should have these values:
```
OS_NAME=`uname`
OSNAME=${OS_NAME}
```

And, also:
* add `${CLASTOOL}/bin/${OSNAME}` to your `PATH` variable
* add `${ANALYSER}/include` and `${CLASTOOL}/include` to your `ROOT_INCLUDE_PATH` variable
* add `${ANALYSER}/slib` and `${CLASTOOL}/slib/${OS_NAME}` to your `LD_LIBRARY_PATH`

## Example for Bash

If you're using **Bash** as your Unix shell, you only need to add the following lines at the end of your `.bashrc` file located in
your home directory. **Note:** here I previously defined another environment variable called `TOPDIR`, which stands for a directory
where all the related repositories are located.

```
export OS_NAME=`uname`
export OSNAME=${OS_NAME}

export CLASTOOL=${TOPDIR}/ClasTool
export CLAS_LIB=${TOPDIR}/clas_lib
export CLAS_PACK=${TOPDIR}/clas_pack

export PATH=${CLASTOOL}/bin/${OSNAME}:${PATH}
export ROOT_INCLUDE_PATH=${CLASTOOL}/include:${ROOT_INCLUDE_PATH}
export LD_LIBRARY_PATH=${CLASTOOL}/slib/${OS_NAME}:${LD_LIBRARY_PATH}
```

For this to take effect, remember to reload your bash session by closing and opening your terminal session or by executing:

```
source .bashrc
```

## Compilation

Just execute `make` in the current directory.

## Integration with ROOT command console

Create an empty text file called `rootlogon.C` in your home directory. This file contains the instructions to run at the beginning of each **ROOT** console session. Inside the file, you should add this content:

```
{
  gSystem->Load("libMathMore");
  gSystem->Load("libClasTool");
}
```

After saving the `rootlogon.C` file, for this to take effect, you need to create another empty text file called `.rootrc` in your home directory as well.

```
Rint.Logon: ~/rootlogon.C
```
This step is option if you keep `rootlogon.C` in the same file where you open you ROOT session.

## Debug for ROOT

From **ROOT version 6.14** onwards, it is necessary to copy all dictionaries files into the dynamic libraries folders `slib/`. To prevent the warning messages, inside **ClasTool** directory, run:

```
find . -name *.pcm -exec cp -t ./slib/Linux {} +
```

## Additional documentation
See [README.ClasTool](README.ClasTool)

