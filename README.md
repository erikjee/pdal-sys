## PDAL CAPI

https://github.com/PDAL/CAPI

## ObtainProjectVersion

```
# We use tags with the three version numbers
	# Use the remainder of the `git describe` output for the build ID
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
