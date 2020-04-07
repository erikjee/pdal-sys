## Install libpdalc

Note: before running the commands below you may first need to patch ObtainProjectVersion.

Also requires ``` pdal ``` and ``` lcov ```. 

```bash
git clone https://github.com/PDAL/CAPI.git 
mkdir CAPI/build && cd CAPI/build
cmake ..
make
make install
```

Verify you can now call pdalc by running 

``` cargo test ```

## Patch ObtainProjectVersion

ObtainProjectVersion assumes a three part version number for pdal. When your pdal version has two parts (e.g. 1.8) the build fails.

It will work when the patch part is ignored in ``` CAPI/cmake/ObtainProjectVersion.cmake ```

```
	#if(GIT_DESCRIBE_OUTPUT MATCHES "^([0-9]+)\\.([0-9]+)\\.([0-9]+)-([0-9]+)-g([a-f0-9]+)$")
	if(GIT_DESCRIBE_OUTPUT MATCHES "^([0-9]+)\\.([0-9]+)-([0-9]+)-g([a-f0-9]+)$")
		string(REGEX REPLACE "([0-9]+).*" "\\1" MAJOR_VERSION ${GIT_DESCRIBE_OUTPUT})
		string(REGEX REPLACE "([0-9]+)\\.([0-9]+).*" "\\2" MINOR_VERSION ${GIT_DESCRIBE_OUTPUT})
		#string(REGEX REPLACE "([0-9]+)\\.([0-9]+)\\.([0-9]+).*" "\\3" PATCH_VERSION ${GIT_DESCRIBE_OUTPUT})
		string(REGEX REPLACE ".*-(.*)-.*" "\\1" COMMIT_COUNT ${GIT_DESCRIBE_OUTPUT})
		string(REGEX REPLACE ".*-g(.*)" "\\1" COMMIT_ID ${GIT_DESCRIBE_OUTPUT})
		set(BUILD_ID "build ${COMMIT_COUNT} (${COMMIT_ID})")
	else()
	message(WARNING "Could not derive version and build ID: 'git describe' command output was \"${GIT_DESCRIBE_OUTPUT}\" - ${GIT_DESCRIBE_ERROR}")
	endif()
  ```
