<template>
    <Page class="page">
        <ActionBar class="action-bar" backgroundColor="#117cd4"
            android.icon="res://icon" android.iconVisibility="always">
            <StackLayout orientation="horizontal"
                ios:horizontalAlignment="center"
                android:horizontalAlignment="center">
                <!-- <Image src="res://nativescript_logo" class="action-image"></Image> -->
                <Label fontSize="16" text="BurisTestApp" color="blacked"
                    class="action-label">
                </Label>

            </StackLayout>
            <ActionItem ios.systemIcon="16"
                android.systemIcon="ic_menu_agenda" @tap="onOpenDrawerTap()"
                ios.position="right" android.position="right">
            </ActionItem>
        </ActionBar>

        <RadSideDrawer ref="drawer">
            <StackLayout ~drawerContent backgroundColor="gray">
                <StackLayout height="56"
                    style="text-align: center; vertical-align: center;">
                    <Label text="Navigation Menu" />
                </StackLayout>
                <StackLayout>
                    <Label text="Primary" padding="10"
                        backgroundColor="lightgray" />
                    <Label text="Social" padding="10" />
                    <Label text="Promotions" padding="10" />
                    <Label text="Labels" padding="10"
                        backgroundColor="lightgray" />
                    <Label text="Important" padding="10" />
                    <Label text="Starred" padding="10" />
                    <Label text="Sent Mail" padding="10" />
                    <Label text="Drafts" padding="10" />
                </StackLayout>
                <Label text="Close" color="lightgray" padding="10"
                    style="horizontal-align: center"
                    @tap="onCloseDrawerTap" />
            </StackLayout>

            <StackLayout ~mainContent>
                <TabView height="100%" androidTabsPosition="bottom"
                    iosIconRenderingMode="alwaysOriginal"
                    tabBackgroundColor="#117cd4" tabTextFontSize="16"
                    tabTextFontSize="16"
                    androidSelectedTabHighlightColor="green">
                    <TabViewItem title="To Do" iconSource="res://home"
                        color="blacked">


                        <!-- Positions an input field, a button, and the list of tasks in a vertical stack. -->
                        <StackLayout orientation="vertical" width="100%"
                            height="100%">

                            <GridLayout columns="2*,*" rows="*" width="100%"
                                height="25%">
                                <!-- Configures the text field and ensures that pressing Return on the keyboard produces the same result as tapping the button. -->
                                <TextField col="0" row="0"
                                    v-model="textFieldValue"
                                    hint="Type new task..." editable="true"
                                    @returnPress="onButtonTap" />

                                <Button col="1" row="0" text="Add task"
                                    @tap="onButtonTap" />
                            </GridLayout>

                            <ListView class="list-group" for="todo in todos"
                                @itemTap="onItemTap" style="height:75%">
                                <v-template>
                                    <Label :text="todo.name"
                                        class="list-group-item-heading"
                                        textWrap="true" />
                                </v-template>
                            </ListView>
                        </StackLayout>
                    </TabViewItem>

                    <TabViewItem title="Completed" iconSource="res://home">
                        <Label
                            text="This tab will list completed tasks for tracking."
                            textWrap="true" />
                    </TabViewItem>

                    <TabViewItem title="Calendar" iconSource="res://home">
                        <Label text="Calendar" textWrap="true" />
                    </TabViewItem>

                </TabView>
            </StackLayout>
        </RadSideDrawer>

    </Page>
</template>

<script>
    import Vue from "nativescript-vue";
    import RadSideDrawer from "nativescript-ui-sidedrawer/vue";
    Vue.use(RadSideDrawer);

    export default {
        methods: {
            onOpenDrawerTap() {
                this.$refs.drawer.nativeView.showDrawer();
            },
            onCloseDrawerTap() {
                this.$refs.drawer.nativeView.closeDrawer();
            },

            onItemTap: function(args) {
                console.log("Item with index: " + args.index + " tapped");
            },

            onButtonTap() {
                if (this.textFieldValue === "")
            return; // Prevents users from entering an empty string.
                console.log("New task added: " + this.textFieldValue +
                "."); // Logs the newly added task in the console for debugging.
                this.todos.unshift({
                    name: this.textFieldValue
                }); // Adds tasks in the ToDo array. Newly added tasks are immediately shown on the screen.
                this.textFieldValue =
                ""; // Clears the text field so that users can start adding new tasks immediately.
            }
        },

        data() {
            return {
                mainContentText: "SideDrawer for NativeScript can be easily setup in the XML definition of your page by defining main- and drawer-content. The component" +
                    " has a default transition and position and also exposes notifications related to changes in its state. Swipe from left to open side drawer.",

                todos: [],
                selectedIndex: 0,
                textFieldValue: ""
            };
        }
    };
</script>

<style scoped>
    .icon {
        font-family: 'icomoon';
    }

    .description-label {
        margin-bottom: 15;
    }

    .home-panel {
        vertical-align: center;
        font-size: 20;
        margin: 15;
    }
</style>