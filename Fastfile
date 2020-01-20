# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

opt_out_usage # opt-out of metrics collection

default_platform(:ios)

platform :ios do
  desc "Push a new beta build to TestFlight"
  lane :beta do
    
    xcversion(version: "11.3.1")
    update_fastlane
    clear_derived_data
    cocoapods
    #increment_build_number
    #xcclean

    # Build & Archive
    gym(clean: true, suppress_xcode_output: true, workspace: "<your_workspace_file_name>.xcworkspace", scheme: "<your_scheme_name>")

    # Only Build
    # xcbuild(clean: true, suppress_xcode_output: true, workspace: "<your_workspace_file_name>.xcworkspace", scheme: "<your_scheme_name>")
    
    # # Upload
    # crashlytics(
    #   api_token: '<api_token>',
    #   build_secret: '<build_secret>',
    #   notes: "Build at " + ENV["BUILD_NUMBER"],
    #   notes_path: 'build/change.log',
    #   groups: "all",
    #   notifications: true
    # )

    # Submit to iTunes Connect (upload_to_testflight)
    pilot(skip_submission: true, skip_waiting_for_build_processing: true)

    upload_symbols_to_crashlytics # Upload dSYM symbolication files to Crashlytics
  end
end
