#
# Copyright (c) 2015 Pavlo Lavrenenko
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#

cmake_minimum_required(VERSION 3.9)
project (SVDLL)

set (SVDLL_LIBRARY server)

if(NOT MSVC)
	add_compile_options(-fno-exceptions) # GCC/Clang flag
	add_compile_options(-fno-rtti) # GCC/Clang flag
	add_compile_options(-Wno-invalid-offsetof) # GCC/Clang flag
	add_compile_options(-fvisibility=hidden) # GCC/Clang flag
	add_definitions(-D_LINUX) # It seems enough for all non-Win32 systems
	add_definitions(-Dstricmp=strcasecmp -Dstrnicmp=strncasecmp -D_snprintf=snprintf -D_vsnprintf=vsnprintf )
	if(CMAKE_BUILD_TYPE MATCHES "Release"
		OR (CMAKE_BUILD_TYPE MATCHES "RelWithDebInfo"
		AND CMAKE_SYSTEM_NAME STREQUAL "Android"))
		add_compile_options(-fno-unwind-tables -fno-asynchronous-unwind-tables) # GCC/Clang flag
		add_compile_options(-fomit-frame-pointer) # GCC/Clang flag
		add_compile_options(-ftree-vectorize) # GCC/Clang flag
		add_compile_options(-funsafe-math-optimizations) # GCC/Clang flag
	endif()
else()
	add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_CRT_NONSTDC_NO_DEPRECATE)
endif()

set (SVDLL_SOURCES
	wpn_shared/disc_weapon_disc.cpp
        activity.h
        activitymap.h
        airtank.cpp
        animating.cpp
        animation.cpp
        animation.h
        basemonster.h
        bmodels.cpp
        buttons.cpp
        cbase.cpp
        cbase.h
        cdll_dll.h
        client.cpp
        client.h
        combat.cpp
        decals.h
        disc_arena.cpp
        disc_arena.h
        disc_objects.h
        disc_powerups.cpp
        disc_weapon.h
        discwar.h
        doors.cpp
        doors.h
        effects.cpp
        effects.h
        enginecallback.h
        explode.cpp
        explode.h
        extdll.h
        func_break.cpp
        func_break.h
        func_tank.cpp
        game.cpp
        game.h
        gamerules.cpp
        gamerules.h
        ggrenade.cpp
        globals.cpp
        h_ai.cpp
        h_battery.cpp
        h_cycler.cpp
        h_export.cpp
        healthkit.cpp
        items.cpp
        items.h
        lights.cpp
        maprules.cpp
        maprules.h
        monsterevent.h
        monsters.h
        mortar.cpp
        mp.def
        mpstubb.cpp
        multiplay_gamerules.cpp
        nodes.h
        observer.cpp
        pathcorner.cpp
        plane.cpp
        plane.h
        plats.cpp
        player.cpp
        player.h
        saverestore.h
        schedule.h
        scriptevent.h
        singleplay_gamerules.cpp
        skill.cpp
        skill.h
        sound.cpp
        soundent.cpp
        soundent.h
        spectator.cpp
        spectator.h
        subs.cpp
        talkmonster.h
        teamplay_gamerules.cpp
        teamplay_gamerules.h
        trains.h
        triggers.cpp
        util.cpp
        util.h
        vector.h
        weapons.cpp
        weapons.h
        world.cpp
        wpn_shared
		xen.cpp
		)
