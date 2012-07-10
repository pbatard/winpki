SUBDIRS = src
TARGET  = pki

# This step produces the UPX compressed and signed releases that are made available for public download
release: all
	@mv src/$(TARGET)$(EXEEXT) .
	@$(STRIP) $(TARGET)$(EXEEXT)
