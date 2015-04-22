# temporary workaround
set(ASSIMP_ENABLE_BOOST_WORKAROUND YES)
set(ASSIMP_BUILD_TEST NO)

if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup()
    fips_project(fips-assimp)
endif()

option(ASSIMP_C4D "Enable C4D Support (windows only)" OFF)
fips_begin_lib(assimp)
    include_directories(.)
    include_directories(assimp/code)
    include_directories(assimp/include)
    include_directories(assimp/code/BoostWorkaround)
    fips_dir(.)
    fips_files(revision.h)
    fips_dir(assimp/include/assimp)
    fips_files(ai_assert.h anim.h camera.h cexport.h
        cfileio.h cimport.h color4.h color4.inl
        config.h DefaultLogger.hpp defs.h
        Exporter.hpp importerdesc.h Importer.hpp
        IOStream.hpp IOSystem.hpp light.h
        Logger.hpp LogStream.hpp material.h
        material.inl matrix3x3.h matrix3x3.inl
        matrix4x4.h matrix4x4.inl mesh.h
        metadata.h NullLogger.hpp postprocess.h
        ProgressHandler.hpp quaternion.h
        quaternion.inl scene.h texture.h
        types.h vector2.h vector2.inl vector3.h
        vector3.inl version.h
    )
    fips_dir(assimp/include/assimp/Compiler)
    fips_files(poppack1.h pstdint.h pushpack1.h)
    fips_dir(assimp/code)
    fips_files(
        Version.cpp
        DefaultIOStream.cpp
        MaterialSystem.h
        MaterialSystem.cpp
        3DSExporter.h
        BlenderIntermediate.h
        COBScene.h
        PretransformVertices.cpp
        IFCMaterial.cpp
        FBXDocument.cpp
        CSMLoader.h
        BlenderDNA.cpp
        STEPFileReader.cpp
        PlyExporter.cpp
        FBXTokenizer.h
        ObjFileImporter.cpp
        BlenderTessellator.h
        BlenderDNA.inl
        STEPFile.h
        SpatialSort.cpp
        MDLFileData.h
        COBLoader.cpp
        LWOLoader.cpp
        STLLoader.h
        DefaultIOStream.h
        FBXParser.cpp
        HMPFileData.h
        BlenderModifier.h
        FBXImporter.h
        JoinVerticesProcess.cpp
        StdOStreamLogStream.h
        DefaultIOSystem.h
        RawLoader.cpp
        IFCReaderGen.h
        Q3BSPFileParser.h
        3DSHelper.h
        BVHLoader.h
        StringComparison.h
        UnrealLoader.h
        OptimizeMeshes.h
        IFCCurve.cpp
        StandardShapes.cpp
        Q3DLoader.h
        ConvertToLHProcess.cpp
        IFCUtil.cpp
        LWSLoader.cpp
        SplitLargeMeshes.h
        Assimp.cpp
        JoinVerticesProcess.h
        BlenderBMesh.cpp
        STLExporter.h
        SmoothingGroups.inl
        OptimizeGraph.cpp
        ProcessHelper.h
        FBXDocumentUtil.cpp
        ParsingUtils.h
        OFFLoader.cpp
        Profiler.h
        ACLoader.cpp
        SortByPTypeProcess.h
        AssbinExporter.h
        SpatialSort.h
        Bitmap.cpp
        IFCProfile.cpp
        SGSpatialSort.h
        irrXMLWrapper.h
        XMLTools.h
        CInterfaceIOWrapper.h
        STEPFileEncoding.cpp
        ScenePreprocessor.h
        FBXUtil.cpp
        RemoveVCProcess.cpp
        Q3BSPFileParser.cpp
        FBXDeformer.cpp
        Vertex.h
        SMDLoader.cpp
        ImproveCacheLocality.cpp
        ObjExporter.h
        XFileHelper.h
        ColladaHelper.h
        DefaultLogger.cpp
        TriangulateProcess.h
        OgreImporter.h
        FBXAnimation.cpp
        OgreXmlSerializer.cpp
        XFileExporter.h
        RemoveComments.cpp
        Q3BSPFileData.h
        SmoothingGroups.h
        XFileExporter.cpp
        IFCReaderGen.cpp
        OgreBinarySerializer.cpp
        AssimpCExport.cpp
        FixNormalsStep.h
        makefile.mingw
        TriangulateProcess.cpp
        OgreMaterial.cpp
        Importer.h
        STEPFileReader.h
        SMDLoader.h
        BaseImporter.h
        OgreBinarySerializer.h
        SkeletonMeshBuilder.h
        VertexTriangleAdjacency.cpp
        ConvertToLHProcess.h
        CalcTangentsProcess.h
        BlenderBMesh.h
        BlenderLoader.cpp
        Q3BSPFileImporter.cpp
        BlenderScene.h
        LWOMaterial.cpp
        FBXUtil.h
        DefaultIOSystem.cpp
        GenFaceNormalsProcess.h
        ComputeUVMappingProcess.h
        FindInstancesProcess.cpp
        ValidateDataStructure.cpp
        ASELoader.h
        SortByPTypeProcess.cpp
        ByteSwapper.h
        LimitBoneWeightsProcess.cpp
        MakeVerboseFormat.h
        UnrealLoader.cpp
        SGSpatialSort.cpp
        ValidateDataStructure.h
        IFCLoader.h
        FBXImportSettings.h
        SplitLargeMeshes.cpp
        RemoveVCProcess.h
        PlyLoader.h
        NFFLoader.cpp
        BlenderLoader.h
        BlenderDNA.h
        XFileImporter.cpp
        OgreStructs.h
        ObjExporter.cpp
        FileLogStream.h
        NFFLoader.h
        PlyParser.h
        Subdivision.h
        XFileImporter.h
        Exceptional.h
        IFCOpenings.cpp
        SceneCombiner.h
        ColladaExporter.h
        ACLoader.h
        OgreParsingUtils.h
        MemoryIOWrapper.h
        B3DImporter.cpp
        LWOBLoader.cpp
        StreamWriter.h
        Q3DLoader.cpp
        FindInvalidDataProcess.cpp
        IRRMeshLoader.h
        IFCBoolean.cpp
        DXFLoader.h
        BlenderTessellator.cpp
        MD5Loader.cpp
        LWOLoader.h
        IRRLoader.h
        IRRMeshLoader.cpp
        ColladaExporter.cpp
        ImporterRegistry.cpp
        FindInstancesProcess.h
        Exporter.cpp
        MS3DLoader.cpp
        TargetAnimation.h
        fast_atof.h
        DXFLoader.cpp
        Importer.cpp
        AssbinLoader.h
        VertexTriangleAdjacency.h
        Q3BSPZipArchive.h
        assbin_chunks.h
        AssxmlExporter.h
        MD4FileData.h
        3DSLoader.cpp
        DeboneProcess.cpp
        FBXProperties.cpp
        ObjFileMtlImporter.cpp
        FBXModel.cpp
        FindInvalidDataProcess.h
        RawLoader.h
        ScenePrivate.h
        OgreStructs.cpp
        Subdivision.cpp
        PlyExporter.h
        BaseImporter.cpp
        BlobIOSystem.h
        Hash.h
        StreamReader.h
        SplitByBoneCountProcess.cpp
        IFCGeometry.cpp
        MDCLoader.cpp
        Q3BSPFileImporter.h
        PolyTools.h
        MS3DLoader.h
        FBXBinaryTokenizer.cpp
        XFileParser.h
        MDLMaterialLoader.cpp
        HMPLoader.h
        TinyFormatter.h
        SkeletonMeshBuilder.cpp
        Q3BSPZipArchive.cpp
        TextureTransform.cpp
        MDCFileData.h
        FBXTokenizer.cpp
        MD2NormalTable.h
        TerragenLoader.cpp
        AssxmlExporter.cpp
        ColladaParser.cpp
        RemoveComments.h
        TargetAnimation.cpp
        ColladaLoader.cpp
        OFFLoader.h
        MDCNormalTable.h
        FixNormalsStep.cpp
        ASEParser.h
        ObjTools.h
        DeboneProcess.h
        MD2FileData.h
        MD2Loader.cpp
        FileSystemFilter.h
        XGLLoader.cpp
        MD3FileData.h
        FindDegenerates.h
        3DSConverter.cpp
        FBXDocumentUtil.h
        COBLoader.h
        MakeVerboseFormat.cpp
        FBXMeshGeometry.cpp
        HalfLifeFileData.h
        FBXParser.h
        ComputeUVMappingProcess.cpp
        IFF.h
        FBXProperties.h
        GenFaceNormalsProcess.cpp
        LWOAnimation.cpp
        NDOLoader.cpp
        NDOLoader.h
        STEPFileEncoding.h
        MDCLoader.h
        DefaultProgressHandler.h
        CalcTangentsProcess.cpp
        3DSExporter.cpp
        GenVertexNormalsProcess.cpp
        AssbinExporter.cpp
        LimitBoneWeightsProcess.h
        ScenePreprocessor.cpp
        CSMLoader.cpp
        ObjFileParser.h
        FBXMaterial.cpp
        ObjFileMtlImporter.h
        ASEParser.cpp
        ObjFileImporter.h
        FBXImporter.cpp
        BaseProcess.h
        BlenderModifier.cpp
        FBXConverter.h
        AssbinLoader.cpp
        GenericProperty.h
        OptimizeGraph.h
        LogAux.h
        OptimizeMeshes.cpp
        SceneCombiner.cpp
        HMPLoader.cpp
        MD3Loader.h
        LineSplitter.h
        IFCUtil.h
        XFileParser.cpp
        ObjFileData.h
        MDLDefaultColorMap.h
        FBXConverter.cpp
        IRRShared.h
        ImproveCacheLocality.h
        FBXCompileConfig.h
        Bitmap.h
        DXFHelper.h
        PlyLoader.cpp
        OgreImporter.cpp
        PostStepRegistry.cpp
        RemoveRedundantMaterials.cpp
        IRRShared.cpp
        LWSLoader.h
        STLExporter.cpp
        TextureTransform.h
        FindDegenerates.cpp
        MD5Loader.h
        BVHLoader.cpp
        MD5Parser.cpp
        XGLLoader.h
        StandardShapes.h
        B3DImporter.h
        3DSLoader.h
        PlyParser.cpp
        TerragenLoader.h
        PretransformVertices.h
        ProcessHelper.cpp
        qnan.h
        STLLoader.cpp
        SplitByBoneCountProcess.h
        ObjFileParser.cpp
        RemoveRedundantMaterials.h
        BlenderScene.cpp
        MDLLoader.h
        BlenderSceneGen.h
        LWOAnimation.h
        MD3Loader.cpp
        GenVertexNormalsProcess.h
        FBXNodeAttribute.cpp
        BaseProcess.cpp
        MDLLoader.cpp
        IRRLoader.cpp
        ColladaLoader.h
        LWOFileData.h
        MD5Parser.h
        ASELoader.cpp
        FBXDocument.h
        OgreXmlSerializer.h
        ColladaParser.h
        MD2Loader.h
        IFCLoader.cpp
        OpenGEXImporter.cpp
        OpenGEXImporter.h
        OpenGEXStructs.h
    )
    fips_dir(assimp/code/BoostWorkaround/boost/tuple)
    fips_files(tuple.hpp)
    fips_dir(assimp/code/BoostWorkaround/boost/math)
    fips_files(common_factor_rt.hpp)
    fips_dir(assimp/code/BoostWorkaround/boost)
    fips_files(
        shared_array.hpp
        noncopyable.hpp
        scoped_array.hpp
        foreach.hpp
        scoped_ptr.hpp
        make_shared.hpp
        format.hpp
        lexical_cast.hpp
        timer.hpp
        pointer_cast.hpp
        shared_ptr.hpp
        static_assert.hpp
    )

    # some third party not fipsified
    fips_dir(assimp/contrib/clipper)
    fips_files(clipper.cpp clipper.hpp)
    fips_dir(assimp/contrib/ConvertUTF)
    fips_files(ConvertUTF.c ConvertUTF.h)
    fips_dir(assimp/contrib/irrXML)
    fips_files(CXMLReaderImpl.h heapsort.h irrArray.h irrString.h irrTypes.h irrXML.cpp irrXML.h)
    fips_dir(assimp/contrib/poly2tri/poly2tri)
    fips_files(poly2tri.h)
    fips_dir(assimp/contrib/poly2tri/poly2tri/common)
    fips_files(shapes.cc shapes.h utils.h)
    fips_dir(assimp/contrib/poly2tri/poly2tri/sweep)
    fips_files(advancing_front.cc advancing_front.h cdt.cc cdt.h sweep.cc sweep.h sweep_context.cc sweep_context.h)
    fips_dir(assimp/contrib/unzip)
    fips_files(crypt.h ioapi.c ioapi.h unzip.c unzip.h)
    fips_dir(assimp/contrib/openddlparser/code)
    fips_files(OpenDDLParser.cpp DDLNode.cpp Value.cpp)
    fips_dir(assimp/contrib/openddlparser/include/openddlparser)
    fips_files(OpenDDLParser.h OpenDDLParserUtils.h OpenDDLCommon.h DDLNode.h Value.h)
    include_directories(assimp/contrib/openddlparser/include/)

    if (FIPS_ANDROID)
        fips_dir(assimp/include/assimp/port/AndroidJNI)
        fips_files(AndroidJNIOSystem.h)
        add_definitions(-DASSIMP_BUILD_NO_C4D_IMPORTER)
    elseif (FIPS_MACOS)
        add_definitions(-DFIPS_ASSIMP_MACOS=1 -DASSIMP_BUILD_NO_C4D_IMPORTER)
    elseif (FIPS_WINDOWS)
        add_definitions(-DFIPS_ASSIMP_WINDOWS=1)
        fips_dir(assimp/code/res)
        fips_files(resource.h)

        if (ASSIMP_C4D)
            fips_dir(assimp/code)
            fips_files(
                Win32DebugLogStream.h
                C4DImporter.cpp
                C4DImporter.h
            )
        else()
            add_definition(-DASSIMP_BUILD_NO_C4D_IMPORTER)
        endif()
    elseif (FIPS_LINUX)
        add_definitions(-DFIPS_ASSIMP_LINUX=1 -DASSIMP_BUILD_NO_C4D_IMPORTER)
    endif()
    fips_deps(zlib)
fips_end_lib()

if (FIPS_CLANG)
    set_target_properties(assimp PROPERTIES COMPILE_FLAGS "-Wno-sign-compare -Wno-deprecated-declarations -Wno-unused-function -Wno-unused-variable -Wno-reorder -fexceptions -frtti")
elseif(FIPS_GCC)
    set_target_properties(assimp PROPERTIES COMPILE_FLAGS "-Wno-sign-compare -Wno-deprecated-declarations -Wno-unused-function -Wno-unused-variable -Wno-reorder -fexceptions -frtti")
elseif(FIPS_MSVC)
    set_target_properties(assimp PROPERTIES COMPILE_FLAGS "/wd4152 /wd4204 /wd4242 /wd4244 /wd4668 /wd4996")
endif()

if (NOT FIPS_IMPORT)
    fips_finish()
endif()
