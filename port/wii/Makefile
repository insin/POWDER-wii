#---------------------------------------------------------------------------------
.SUFFIXES:
#---------------------------------------------------------------------------------
ifeq ($(strip $(DEVKITPPC)),)
$(error "Please set DEVKITPPC in your environment. export DEVKITPPC=<path to>devkitPPC")
endif

include $(DEVKITPPC)/wii_rules

#---------------------------------------------------------------------------------
# TARGET is the name of the output
# BUILD is the directory where object files & intermediate files will be placed
# SOURCES is a list of directories containing source code
# INCLUDES is a list of directories containing extra header files
#---------------------------------------------------------------------------------
TARGET		:=	powder

#---------------------------------------------------------------------------------
# any extra libraries we wish to link with the project
#---------------------------------------------------------------------------------
LIBS	:=	-lSDL -lwiiuse -lfat -lbte -logc -lm -lwiikeyboard

#---------------------------------------------------------------------------------
# list of directories containing libraries, this must be the top level containing
# include and lib
#---------------------------------------------------------------------------------
LIBDIRS	:=

#---------------------------------------------------------------------------------
# options for code generation
#---------------------------------------------------------------------------------
CFLAGS = -g -O2 -Wall $(MACHDEP) $(INCLUDE) -DUSING_WII -DUSING_TILE10
CXXFLAGS = $(CFLAGS)
LDFLAGS	=	-g $(MACHDEP) -Wl,-Map,$(notdir $@).map

#---------------------------------------------------------------------------------
# no real need to edit anything past this point unless you need to add additional
# rules for different file extensions
#---------------------------------------------------------------------------------
OUTPUT	:=	$(CURDIR)/$(TARGET)

VPATH	:=

DEPSDIR	:=	$(CURDIR)

CFILES		:=
CPPFILES	:=	wiimain.cpp \
			hamfake.cpp \
			../../action.cpp \
			../../assert.cpp \
			../../ai.cpp \
			../../artifact.cpp \
			../../bmp.cpp \
			../../build.cpp \
			../../buf.cpp \
			../../control.cpp \
			../../creature.cpp \
			../../dpdf_table.cpp \
			../../encyc_support.cpp \
			../../gfxengine.cpp \
			../../grammar.cpp \
			../../hiscore.cpp \
			../../input.cpp \
			../../intrinsic.cpp \
			../../item.cpp \
			../../map.cpp \
			../../mobref.cpp \
			../../msg.cpp \
			../../name.cpp \
			../../piety.cpp \
			../../rand.cpp \
			../../signpost.cpp \
			../../smokestack.cpp \
			../../speed.cpp \
			../../sramstream.cpp \
			../../stylus.cpp \
			../../victory.cpp \
			../../encyclopedia.cpp \
			../../glbdef.cpp \
			../../credits.cpp \
			../../license.cpp \
			../../gfx/all_bitmaps.cpp \
			../../rooms/allrooms.cpp

SFILES		:=
BINFILES	:=

#---------------------------------------------------------------------------------
# use CXX for linking C++ projects, CC for standard C
#---------------------------------------------------------------------------------
LD	:=	$(CXX)

OFILES	:=	$(addsuffix .o,$(BINFILES)) \
			$(CPPFILES:.cpp=.o) $(CFILES:.c=.o) $(SFILES:.s=.o)

DEPENDS	:=	$(OFILES:.o=.d)

#---------------------------------------------------------------------------------
# build a list of include paths
#---------------------------------------------------------------------------------
INCLUDE	:=	$(foreach dir,$(INCLUDES), -iquote $(CURDIR)/$(dir)) \
			$(foreach dir,$(LIBDIRS),-I$(dir)/include) \
			-I$(CURDIR)/$(BUILD) \
			-I$(LIBOGC_INC) \
			-I$(LIBOGC_INC)/SDL

#---------------------------------------------------------------------------------
# build a list of library paths
#---------------------------------------------------------------------------------
LIBPATHS	:=	$(foreach dir,$(LIBDIRS),-L$(dir)/lib) \
				-L$(LIBOGC_LIB)

#---------------------------------------------------------------------------------
$(BUILD):
	@[ -d $@ ] || mkdir -p $@
	@make --no-print-directory -C $(BUILD) -f $(CURDIR)/Makefile

#---------------------------------------------------------------------------------
# main targets
#---------------------------------------------------------------------------------
$(OUTPUT).dol: $(OUTPUT).elf
$(OUTPUT).elf: $(OFILES)

-include $(DEPENDS)

#---------------------------------------------------------------------------------
run:
	wiiload $(TARGET).dol

#---------------------------------------------------------------------------------
clean:
	@echo clean ...
	rm -f $(OFILES) $(DEPENDS) $(OUTPUT).elf $(OUTPUT).dol
