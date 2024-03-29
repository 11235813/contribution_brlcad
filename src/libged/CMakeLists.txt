
# Macro for adding commands to libged.  Use in the command subdirectory as follows:
#
# GED_ADD_CMD(CMD_SRCS CMD_INCLUDES CMD_LIBS)
#
# with the last two arguments being optional.
MACRO(GED_ADD_CMD sources)
  get_filename_component(currentdir ${CMAKE_CURRENT_SOURCE_DIR} NAME)
  foreach(srcfile ${${sources}})
    LIST(APPEND cmd_srcs "${currentdir}/${srcfile}")
  endforeach(srcfile ${${sources}})
  set(LIBGED_CMD_SRCS ${LIBGED_CMD_SRCS} ${cmd_srcs} CACHE INTERNAL "libged cmd srcs" FORCE)
  if(${ARGV1})
    set(LIBGED_CMD_INCLUDE_DIRS ${LIBGED_CMD_INCLUDE_DIRS} ${${ARGV1}})
    LIST(REMOVE_DUPLICATES LIBGED_CMD_INCLUDE_DIRS)
    set(LIBGED_CMD_INCLUDE_DIRS ${LIBGED_CMD_INCLUDE_DIRS} CACHE INTERNAL "libged cmd includes" FORCE)
  endif(${ARGV1})
  if(${ARGV2})
    set(LIBGED_CMD_LIBS_LIST ${LIBGED_CMD_LIBS_LIST} ${${ARGV2}}) 
    LIST(REMOVE_DUPLICATES LIBGED_CMD_LIBS_LIST)
    set(LIBGED_CMD_LIBS_LIST ${LIBGED_CMD_LIBS_LIST} CACHE INTERNAL	"libged cmd libs" FORCE)
  endif(${ARGV2})
ENDMACRO(GED_ADD_CMD)

# if this subdir stuff is pushed into the actual subdirs, the autoconf vs cmake
# verification (sh/cmakecheck.sh) will fail on dist-hook.
if(BULLET_FOUND)
  GED_ADD_CMD(LIBGED_SIM_SOURCES BULLET_INCLUDE_DIR BULLET_LIBRARIES)
  set(SIM_SRCS 
    simulate/simphysics.cpp 
    simulate/simulate.c
    simulate/simcollisionalgo.cpp 
    simulate/simutils.c 
    simulate/simrt.c
    )
  CMAKEFILES(simulate/simrt.h simulate/simutils.h)
else(BULLET_FOUND)
  set(SIM_SRCS "")
  set(ged_ignore_files simulate/simphysics.cpp simulate/simulate.c simulate/simcollisionalgo.cpp simulate/simcollisionalgo.h simulate/simutils.c simulate/simrt.c simulate/simrt.h simulate/simutils.h)
endif(BULLET_FOUND)

set(AVOID_SRCS dag.cpp)

set(LIBGED_SOURCES
  3ptarb.c
  adc.c
  adjust.c
  ae2dir.c
  aet.c
  analyze.c
  annotate.c
  arb.c
  arced.c
  arot.c
  attr.c
  autoview.c
  bb.c
  bev.c
  bigE.c
  blast.c
  bo.c
  bot.c
  bot_condense.c
  bot_decimate.c
  bot_dump.c
  bot_face_fuse.c
  bot_face_sort.c
  bot_fuse.c
  bot_flip.c
  bot_merge.c
  bot_smooth.c
  bot_split.c
  bot_sync.c
  bot_vertex_fuse.c
  brep.c
  cat.c
  cc.c
  center.c
  clip.c
  clone.c
  color.c
  comb.c
  comb_color.c
  comb_std.c
  combmem.c
  concat.c
  copy.c
  copyeval.c
  copymat.c
  cpi.c
  dbip.c
  debugbu.c
  debugdir.c
  debuglib.c
  debugmem.c
  debugnmg.c
  decompose.c
  delay.c
  dg_obj.c
  dir2ae.c
  draw.c
  dump.c
  dup.c
  eac.c
  echo.c
  edbot.c
  edcodes.c
  edcomb.c
  edit.c
  editit.c
  edmater.c
  edpipe.c
  erase.c
  exists.c
  expand.c
  eye.c
  eye_pos.c
  facetize.c
  fb2pix.c
  find.c
  form.c
  fracture.c
  ged.c
  ged_util.c
  get.c
  get_autoview.c
  get_comb.c
  get_eyemodel.c
  get_obj_bounds.c
  get_solid_kp.c
  get_type.c
  glob.c
  globals.c
  gqa.c
  grid.c
  grid2model_lu.c
  grid2view_lu.c
  group.c
  hide.c
  how.c
  human.c
  illum.c
  importFg4Section.c
  inside.c
  instance.c
  isize.c
  item.c
  keep.c
  keypoint.c
  kill.c
  killall.c
  killrefs.c
  killtree.c
  label.c
  list.c
  loadview.c
  log.c
  lookat.c
  ls.c
  lt.c
  m2v_point.c
  make.c
  make_bb.c
  make_name.c
  make_pnts.c
  match.c
  mater.c
  mirror.c
  model2grid_lu.c
  model2view.c
  model2view_lu.c
  move.c
  move_all.c
  move_arb_edge.c
  move_arb_face.c
  mrot.c
  nirt.c
  nmg_collapse.c
  nmg_fix_normals.c
  nmg_simplify.c
  ocenter.c
  open.c
  orient.c
  orotate.c
  oscale.c
  otranslate.c
  overlay.c
  path.c
  pathlist.c
  pathsum.c
  perspective.c
  pix2fb.c
  plot.c
  pmat.c
  pmodel2view.c
  png.c
  polyclip.cpp
  pov.c
  prcolor.c
  prefix.c
  preview.c
  protate.c
  ps.c
  pscale.c
  ptranslate.c
  push.c
  put.c
  put_comb.c
  putmat.c
  qray.c
  quat.c
  qvrot.c
  rcodes.c
  rect.c
  red.c
  regdef.c
  region.c
  remove.c
  report.c
  rfarb.c
  rmap.c
  rmat.c
  rmater.c
  rot.c
  rot_point.c
  rotate_about.c
  rotate_arb_face.c
  rotate_eto.c
  rotate_extrude.c
  rotate_hyp.c
  rotate_tgc.c
  rrt.c
  rt.c
  rtabort.c
  rtcheck.c
  rtwizard.c
  savekey.c
  saveview.c
  scale.c
  scale_ehy.c
  scale_ell.c
  scale_epa.c
  scale_eto.c
  scale_extrude.c
  scale_hyp.c
  scale_part.c
  scale_rhc.c
  scale_rpc.c
  scale_superell.c
  scale_tgc.c
  scale_tor.c
  screengrab.c
  search.c
  select.c
  set_output_script.c
  set_transparency.c
  set_uplotOutputMode.c
  setview.c
  shaded_mode.c
  shader.c
  shells.c
  showmats.c
  size.c
  slew.c
  solids_on_ray.c
  sphgroup.c
  summary.c
  sync.c
  tables.c
  tire.c
  title.c
  tol.c
  tops.c
  tra.c
  trace.c
  track.c
  translate_extrude.c
  translate_tgc.c
  tree.c
  typein.c
  unhide.c
  units.c
  v2m_point.c
  vdraw.c
  version.c
  view.c
  view2grid_lu.c
  view2model.c
  view2model_lu.c
  view2model_vec.c
  view_obj.c
  viewdir.c
  voxelize.c
  vrot.c
  vutil.c
  wcodes.c
  wdb_bigE.c
  wdb_comb_std.c
  wdb_importFg4Section.c
  wdb_nirt.c
  wdb_obj.c
  wdb_qray.c
  wdb_track.c
  wdb_vdraw.c
  whatid.c
  which.c
  which_shader.c
  who.c
  wmater.c
  xpush.c
  ypr.c
  zap.c
  zoom/zoom.c
  ${SIM_SRCS}
  ${AVOID_SRCS}
  )

# Core logic for adding commands to the libged source/lib/include lists.
file(GLOB GED_DIR_CONTENTS ${CMAKE_CURRENT_SOURCE_DIR} *)
foreach(item ${GED_DIR_CONTENTS})
  get_filename_component(item_name ${item} NAME)
  if(IS_DIRECTORY ${item} AND NOT ${item_name} STREQUAL "libged" AND NOT ${item_name} STREQUAL ".svn")
    LIST(APPEND ged_subdirs ${item_name})
  endif(IS_DIRECTORY ${item} AND NOT ${item_name} STREQUAL "libged" AND NOT ${item_name} STREQUAL ".svn")
endforeach(item ${GED_DIR_CONTENTS})
foreach(item ${ged_subdirs})
  if(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${item}/CMakeLists.txt)
    add_subdirectory(${item})
  endif(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${item}/CMakeLists.txt)
endforeach(item ${ged_subdirs})
set(LIBGED_SOURCES ${LIBGED_SOURCES} ${LIBGED_CMD_SRCS})
if(LIBGED_CMD_LIBS_LIST)
  LIST(REMOVE_DUPLICATES LIBGED_CMD_LIBS_LIST)
endif(LIBGED_CMD_LIBS_LIST)
if(LIBGED_CMD_INCLUDE_DIRS)
  LIST(REMOVE_DUPLICATES LIBGED_CMD_INCLUDE_DIRS)
endif(LIBGED_CMD_INCLUDE_DIRS)


# Include directories needed by libged users
set(GED_INCLUDE_DIRS
  ${BRLCAD_BINARY_DIR}/include
  ${BRLCAD_SOURCE_DIR}/include
  ${ANALYZE_INCLUDE_DIRS}
  ${BU_INCLUDE_DIRS}
  ${FB_INCLUDE_DIRS}
  ${RT_INCLUDE_DIRS}
  ${WDB_INCLUDE_DIRS}
  )

# Local include directories
# includes from plugins
set(GED_LOCAL_INCLUDE_DIRS
  ${PNG_INCLUDE_DIR}
  ${LIBGED_CMD_INCLUDE_DIRS}
  ${REGEX_INCLUDE_DIR}
  )
# local includes
set(GED_LOCAL_INCLUDE_DIRS
  ${GED_LOCAL_INCLUDE_DIRS}
  ${CLIPPER_INCLUDE_DIR}
  )

BRLCAD_LIB_INCLUDE_DIRS(ged GED_INCLUDE_DIRS GED_LOCAL_INCLUDE_DIRS)

if(CPP_DLL_DEFINES)
  add_definitions(-DCLIPPER_DLL_IMPORTS)
endif(CPP_DLL_DEFINES)

if(BULLET_FOUND)
  if(ADAPTAGRAMS_FOUND)
    BRLCAD_ADDLIB(libged "${LIBGED_SOURCES}" "libwdb;librt;libfb;libbu;libicv;libanalyze;${AVOID_LIBRARY};${LIBGED_CMD_LIBS_LIST};${REGEX_LIBRARY};${WINSOCK_LIB};${CLIPPER_LIBRARY};${M_LIBRARY}" NOSTRICTCXX)
  else(ADAPTAGRAMS_FOUND)
    BRLCAD_ADDLIB(libged "${LIBGED_SOURCES}" "libwdb;librt;libfb;libbu;libicv;libanalyze;${LIBGED_CMD_LIBS_LIST};${REGEX_LIBRARY};${WINSOCK_LIB};${CLIPPER_LIBRARY};${M_LIBRARY}" NOSTRICTCXX)
  endif(ADAPTAGRAMS_FOUND)
else(BULLET_FOUND)
  if(ADAPTAGRAMS_FOUND)
    BRLCAD_ADDLIB(libged "${LIBGED_SOURCES}" "libwdb;librt;libfb;libbu;libicv;libanalyze;${AVOID_LIBRARY};${LIBGED_CMD_LIBS_LIST};${REGEX_LIBRARY};${WINSOCK_LIB};${CLIPPER_LIBRARY};${M_LIBRARY}")
  else(ADAPTAGRAMS_FOUND)
    BRLCAD_ADDLIB(libged "${LIBGED_SOURCES}" "libwdb;librt;libfb;libbu;libicv;libanalyze;${LIBGED_CMD_LIBS_LIST};${REGEX_LIBRARY};${WINSOCK_LIB};${CLIPPER_LIBRARY};${M_LIBRARY}")
  endif(ADAPTAGRAMS_FOUND)
endif(BULLET_FOUND)
SET_TARGET_PROPERTIES(libged PROPERTIES VERSION 20.0.1 SOVERSION 20)

set(ged_ignore_files
  ${ged_ignore_files}
  ged_private.h
  qray.h
  simulate/simulate.h
  simulate/simcollisionalgo.h
  simulate/simutils.h
  simulate/simrt.h
  wdb_qray.h
  )
CMAKEFILES(${ged_ignore_files})
CMAKEFILES(Makefile.am)

# Local Variables:
# tab-width: 8
# mode: cmake
# indent-tabs-mode: t
# End:
# ex: shiftwidth=2 tabstop=8
