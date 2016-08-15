# cocopods_bitcode_jenkins_support

#### Building your iOS Release build on Jenkins,

#### Inside your podfile

adding the flags below when using cocopods:

    post_install do |installer|
        installer.pods_project.targets.each do |target|
            target.build_configurations.each do |config|
                cflags = config.build_settings['OTHER_CFLAGS'] || ['$(inherited)']
                cflags << '-fembed-bitcode'
                config.build_settings['OTHER_CFLAGS'] = cflags
            end
        end
    end

Or simply removing it:

    post_install do |installer|
        installer.pods_project.targets.each do |target|
            target.build_configurations.each do |config|
                 config.build_settings['ENABLE_BITCODE'] = 'NO'
            end
        end
    end
