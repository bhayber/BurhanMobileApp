<template xmlns:android="">
    <Page class="page">
        <ActionBar class="action-bar">
            <!--
            Use the NavigationButton as a side-drawer button in Android
            because ActionItems are shown on the right side of the ActionBar
            -->
            <NavigationButton ios:visibility="collapsed" icon="res://menu" @tap="onDrawerButtonTap"></NavigationButton>
            <!--
            Use the ActionItem for IOS with position set to left. Using the
            NavigationButton as a side-drawer button in iOS is not possible,
            because its function is to always navigate back in the application.
            -->
            <ActionItem icon="res://menu"
                android:visibility="collapsed"
                @tap="onDrawerButtonTap"
                ios.position="left">
            </ActionItem>
            <Label class="action-bar-title" text="Ramazan's Super App"></Label>
        </ActionBar>

        <StackLayout orientation="vertical" width="100%" height="100%" backgroundColor="lightgray">

            <TabView  androidTabsPosition="bottom"
                      tabTextFontSize="16" tabTextColor="black" tabBackgroundColor="#3a53ff">
                <TabViewItem iconSource="res://outline_event_black_48" title="Calendar">
                    <Label text="Label in Tab 1" />
                </TabViewItem>
                <TabViewItem iconSource="res://outline_event_black_48" title="Notifications">
                    <Label text="Notifications" />
                </TabViewItem>
            </TabView>

        </StackLayout>

    </Page>
</template>

<script>
    import * as utils from "~/shared/utils";
    import SelectedPageService from "../shared/selected-page-service";
    export default {
        mounted() {
            SelectedPageService.getInstance().updateSelectedPage("Home");
        },
        computed: {
            message() {
                return "<!-- Page content goes here -->";
            }
        },
        methods: {
            onDrawerButtonTap() {
                utils.showDrawer();
            }
        }
    };
</script>

<style scoped lang="scss">
    // Start custom common variables
    @import '~@nativescript/theme/scss/variables/blue';
    // End custom common variables

    // Custom styles
</style>
