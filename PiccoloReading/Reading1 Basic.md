# Reading1 - Starting from main()

## 1. main()

Open the solution, under the `Engine\PilotEditor\source` folder, find the `main()` entry point in `main.cpp`

```c++
int main(int argc, char** argv)
{
    std::filesystem::path pilot_root_folder = std::filesystem::path(PILOT_XSTR(PILOT_ROOT_DIR));

    Pilot::EngineInitParams params;
    params.m_root_folder      = pilot_root_folder;
    params.m_config_file_path = pilot_root_folder / "PilotEditor.ini";

    Pilot::PilotEngine::getInstance().startEngine(params);
    Pilot::PilotEngine::getInstance().initialize();
    Pilot::PilotEditor::getInstance().initialize(&(Pilot::PilotEngine::getInstance()));
    Pilot::PilotEditor::getInstance().run();
    Pilot::PilotEditor::getInstance().clear();
    Pilot::PilotEngine::getInstance().clear();
    Pilot::PilotEngine::getInstance().shutdownEngine();
    
    return 0;
}
```

### PilotEngine::startEngine()

```c++
    void PilotEngine::startEngine(const EngineInitParams& param)
    {
        Reflection::TypeMetaRegister::Register();

        ConfigManager::getInstance().initialize(param);
        AssetManager::getInstance().initialize();
        PUIManager::getInstance().initialize();
        WorldManager::getInstance().initialize();
        SceneManager::getInstance().initialize();

        m_tri_frame_buffer.initialize();
        m_renderer->RegisterGetPtr(std::bind(&getFrameBuffer, &m_tri_frame_buffer, std::placeholders::_1));
        m_renderer->RegisterGetPtr(std::bind(&getMemoryFromHandle, std::placeholders::_1));
        m_renderer->RegisterGetPtr(std::bind(&getImageFromHandle, std::placeholders::_1));
        m_renderer->RegisterFuncPtr(std::bind(&addReleaseMeshHandle, std::placeholders::_1));
        m_renderer->RegisterFuncPtr(std::bind(&addReleaseMaterialHandle, std::placeholders::_1));
        m_renderer->RegisterFuncPtr(std::bind(&addReleaseSkeletonBindingHandle, std::placeholders::_1));
        m_renderer->initialize();

        LOG_INFO("engine start");
    }
```

